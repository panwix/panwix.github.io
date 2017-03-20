---
layout: post
title: 开发继承GenericUDf的UDF
categories:  大数据平台架构
tags: [hive]
fullview: true
---

# 开发继承GenericUDf的UDF

### 一、简述
继承org.apache.hadoop.hive.ql.udf.generic.GenericUDF之后，需要重写几个重要的方法：<br>

`public void configure(MapredContext context){}`<br>
//可选，该方法中可以通过context.getJobConf()获取job执行的时候的Configuration；<br>
//可以通过Configuration传递参数值<br>

`public ObjectInspector initialize(ObjectInspector[] arguments)`<br>
//必选，该方法用于函数初始化操作，并定义函数的返回值类型；<br>

`public Object evaluate(DeferredObject[] args){}`
//必选，函数处理的核心方法，用途和UDF中的evaluate一样；

`public String getDisplayString(String[] children){}`
//必选，显示函数的帮助信息

`public void close(){}`
//可选，执行关闭操作

### 二、initialize方法
initialize方法在sql调用udf函数中，首先被调用，它完成下面4件事

1. 验证输入的类型是否预期输入
2. 设置返回值，设置返回一个与预期输出类型相符的ObjectInspector，以下是与java类型相对应的分布式类型：
	* Binary ---> javaBinaryObjectInspector
	* Boolean ---> javaBooleanObjectInspector
	* Byte ---> javaByteObjectInspector
	* Double ---> javaDoubleObjectInspector
	* Float ---> javaFloatObjectInspector
	* Int ---> javaIntObjectInspector
	* Long ---> javaLongObjectInspector
	* Short ---> javaShortObjectInspector
	* String ---> javaStringObjectInspector
	* Timestamp ---> javaTimestampObjectInspector
	* Void ---> javaVoidObjectInspector
	* List、Array ---> StandardListObjectInspector
	* Map ---> StandardMapObjectInspector
	* List、Array ---> StandardStructObjectInspector
3. 存储在全局变量的ObjectInspectors元素的输入
4. 其实第三步不是必须的，因为全局变量能在evaluate方法中以局部变量的形式声明并处理，但是在initlialize存储全局变量，只需要初始化一次。

	注:<br>
	获取传入的List参数`StandardListObjectInspector listOI = (StandardListObjectInspector) arguments[0]`<br>
	返回List<String>类型`return ObjectInspectorFactory.getStandardListObjectInspector( PrimitiveObjectInspectorFactory.writableStringObjectInspector );`<br>
	返回字符串类型`return PrimitiveObjectInspectorFactory.writableStringObjectInspector`

### 三、evaluate方法：处理函数从输入到输出的逻辑，返回函数处理预期结果的值
1. 将输入值，声明局部变量通过initialize方法判断合法的变量存储。
2. 处理函数逻辑，将输入通过代码逻辑得到结果并返回。hive中的变量类型与java中的变量类型相匹配：

	hive类型 | java类型
	----|------
	array<> | ArrayList<>  
	struct<> | Object

### 四、getDisplayString方法
1. 用于explain sql的时候，方便查看其返回的格式
2. 类似于java的toString方法 	

### 五、样例
输入["{\"a\":1}","{\"a\":3}"]
输出["{\"a\":1_new}","{\"a\":3_new}"]

```
package yscredit.udf;

import com.google.gson.Gson;
import org.apache.hadoop.hive.ql.exec.UDFArgumentException;
import org.apache.hadoop.hive.ql.metadata.HiveException;
import org.apache.hadoop.hive.ql.udf.generic.GenericUDF;
import org.apache.hadoop.hive.serde2.objectinspector.*;
import org.apache.hadoop.hive.serde2.objectinspector.primitive.PrimitiveObjectInspectorFactory;
import org.apache.hadoop.hive.serde2.objectinspector.primitive.StringObjectInspector;
import org.apache.hadoop.io.Text;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

/**
 * @author hupanwei
 *
 * transform json array to json array.
 *
 */
public class ArrayToArray extends GenericUDF {

	private ListObjectInspector listoi;
	private StringObjectInspector stringOI;
	private ArrayList<String> valueList = new ArrayList<String>();


	/**
	 * 初始化
	 * @param arguments
	 *
	 * @return
	 * @throws UDFArgumentException
	 */
	@Override
	public ObjectInspector initialize(ObjectInspector[] arguments) throws UDFArgumentException {
		if (arguments.length != 1) {
			throw new UDFArgumentException("The function udfTest(String) takes exactly 1 arguments.");
		}
		listoi = (ListObjectInspector)arguments[0];
		stringOI = ((StringObjectInspector)listoi.getListElementObjectInspector());
		//定义udf的返回类型，这里是List<String>类型
		return ObjectInspectorFactory.getStandardListObjectInspector(
				PrimitiveObjectInspectorFactory.javaStringObjectInspector);
	}

	@Override
	public Object evaluate(DeferredObject[] arguments) throws HiveException {
		valueList.clear();
		// 获取输入参数list的长度
		int nelements = listoi.getListLength(arguments[0].get());
		for(int i=0;i<nelements;i++) {
			//遍历得到list内的所有内容
			Text text = (Text)listoi.getListElement(arguments[0].get(),i);
			//transfrom string to map
			String string = text.toString();
			Gson gson = new Gson();
			Map<String, Object> map = new HashMap<String, Object>();
			map = gson.fromJson(string, map.getClass());
			//Transform the map's value
			for (Object obj : map.keySet()) {
				Object str = map.get(obj);
				int value = (((Double)str).intValue());
				Map mapNew = new HashMap<String, String>();
				mapNew.put(obj, value + "_new");
				valueList.add(mapNew.toString());
			}
		}
		//返回新的List<String>
		return valueList;
	}

	@Override
	public String getDisplayString(String[] arguments) {
		return "do transform the list value";
	}

}
```


### 使用方法
1. 命令行输入`mvn clean install`打包
2. 上传到hdfs
3. 在hive中输入：

		use test;
		drop temporary function array_to_array;
		drop temporary get_json_array;
		delete jar hdfs://ns1/user/hupanwei/udf/test/original-ys-udf-1.0.0-SNAPSHOT.jar
		add jar hdfs://ns1/user/hupanwei/udf/test/original-ys-udf-1.0.0-SNAPSHOT.jar
		create temporary function array_to_array as 'yscredit.udf.ArrayToArray';
		create temporary function get_json_array as 'yscredit.udf.GetJsonArray';
		select array_to_array(get_Json_Array('[{"a":1},{"a":3}]'))
