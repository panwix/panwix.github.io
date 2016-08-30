# DataTables 文档
DataTables是一款jquery表格插件。它是一个高度灵活的工具，可以将任何html表格添加高级的交互功能。

* 分页，即时搜索和排序
* 几乎支持任何数据源：DOM，javascript，Ajax和服务器处理
* 支持不同主题 DataTables，jQuery UI，Bootstrap，Foundation
* 各式各样的扩展：Editor，TableTools，FixedColumns......
* 丰富多样的option和强大的API
* 支持国际化

### 例子
html

   	<table id="example" class="display" cellspacing="0" width="100%"> 
    <thead> 
     <tr> 
      <th></th> 
      <th>序号</th> 
      <th>标题</th> 
      <th>连接</th> 
     </tr> 
    </thead> 
    <tbody></tbody> 
    <tfoot> 
     <tr> 
      <th></th> 
      <th>序号</th> 
      <th>标题</th> 
      <th>连接</th> 
     </tr> 
    </tfoot> 
    <!-- tbody是必须的 --> 
   	</table>
   	
js

	/*Javascript代码片段*/
	var t = $('#example').DataTable({
		"bAutoWidth": false,
		"pagingType":   "full_numbers",
		"language": {
        	"processing": "玩命加载中...",
			"lengthMenu": "显示 _MENU_ 项结果",
			"zeroRecords": "暂无股东及出资信息",
			"info": "共 查询到 _TOTAL_ 条记录    共 _PAGES_ 页 ",
			"infoEmpty": "共 查询到 0 条记录    共 0 页",
			"infoFiltered": "(由 _MAX_ 项结果过滤)",
			"infoPostFix": "",
			"url": "",
			"paginate": {
				"first":    "|<",
				"previous": "<<",
				"next":     ">>",
				"last":     ">|"
			}
	 	},
		"processing" : true,
		"serverSide" : true,
		"ordering":false,
    	ajax: {
        //指定数据源
        url: "http://www.gbtags.com/gb/networks/uploads/a7bdea3c-feaf-4bb5-a3bd-f6184c19ec09/data.txt",
        type: "post"
    	},
    	//每页显示三条数据
    	pageLength: 3,
    	columns: [{
        	"data": null //此列不绑定数据源，用来显示序号
    	},
    	{
        	"data": "id"
    	},
    	{
        	"data": "title"
    	},
    	{
        	"data": "url"
    	}],
    	"columnDefs": [{
    		"targets":7,
			"render":function(data, type, row){
				var dateStamp = convertDate(row.conDate);
				var date = convertDate('2014-03-01');
				if (row.country_CN == "false"){
					return "<span class='clickToDetail' 					onclick=shareHodlerDetail("+"'"+row.inv+"'"+","+"'"+row.invId					+"'"+")>查看</span>";
				}else if(row.country_CN == "true"){
					return "";
				}
			}
    	},
    	{
        "render": function(data, type, row, meta) {
            //渲染 把数据源中的标题和url组成超链接
            return '<a href="' + data + '" target="_blank">' + row.title + '</a>';
        },
        //指定是第三列
        "targets": 2
    	}]

	});

	//前台添加序号
	t.on('order.dt search.dt',
	function() {
    t.column(0, {
        "search": 'applied',
        "order": 'applied'
    }).nodes().each(function(cell, i) {
        cell.innerHTML = i + 1;
    });
	}).draw();

	//更换数据源（相同格式，但是数据内容不同）
	$("#redraw").click(function() {
    var url = table.api().ajax.url("http://www.gbtags.com/gb/networks/uploads/a	7bdea3c-feaf-4bb5-a3bd-f6184c19ec09/newData.txt");
    url.load();
	}); 
	
	
### 自定义Dom显示
* I - Length changing 每页显示多少条数据选项
* f - Filtering input 搜索框
* t - The Table 表格
* i - information  表格信息
* p - Pagination 分页按钮
* r - pRocessing 加载等待显示信息
* < and > - div elements 一个div元素
* < "#id" and > - div width an id 指定id的div元素
* < "class" and > - div with a class 指定样式名的div元素
* < "id.class" and > - div with an id and class 指定id和样式的div元素

example：

	$(document).ready(function() {
    	$('#example').dataTable( {
        	"dom": '<"top"i>rt<"bottom"flp><"clear">'
    	} );
	} ); 
	  	
### 滚动条
	$(document).ready(function() {
     $('#example').dataTable( {
         "scrollY": 200,
         "scrollCollapse": true,
         "jQueryUI": true
     } );
 	} );
 	
### 分页样式
通过pagingType选项来配置分页样式

* simple - 只有上一页，下一页两个按钮
* simple - 除了上一页，下一页两个按钮还有页数按钮，Datatables默认是这个
* full - 有四个按钮首页，上一页，下一页，末页
* full_numbers - 除了首页，上一页,下一页, 末页四个按钮还有页数按钮
* 分页插件：
	1. ellipses：页数带有省略号 	//cdn.datatables.net/plug-ins/1.10.12/pagination/ellipses.js
	2. extjs： 表格样式为extjs  //cdn.datatables.net/plug-ins/1.10.12/pagination/extjs.js 使用方法："sPaginationType": "extStyle"
	3. four_button: 显示4个按钮  //cdn.datatables.net/plug-ins/1.10.12/pagination/four_button.js 使用方法: "sPaginationType": "four_button"
	4. full_numbers_no_ellipses 显示所有页数，没有省略号 //cdn.datatables.net/plug-ins/1.10.12/pagination/full_numbers_no_ellipses.js 使用方法： "pagingType": "full_numbers_no_ellipses"
	5. input: 显示输入框，跳转到输入的页数 //cdn.datatables.net/plug-ins/1.10.12/pagination/input.js 使用方法："pagingType": "input"
	6. scrolling: 页面切换时带有滚动的动画效果 //cdn.datatables.net/plug-ins/1.10.12/pagination/scrolling.js 使用方法： "sPaginationType": "scrolling"
	7. select: 显示选择的行号 //cdn.datatables.net/plug-ins/1.10.12/pagination/select.js
	8. simple_numbers_no_ellipses: 和simple_numbers一样但是没有省略号 //cdn.datatables.net/plug-ins/1.10.12/pagination/simple_numbers_no_ellipses.js
	
### 状态保存
`stateSave: true`   
`stateSaveCallback: true`数据为异步加载  
`stateLoadCallback:true`数据为一部家在
`stateDuration: 4`设置时间

### 功能启用／禁用	
		paging: false,
		ordering: false,
		info: false

### 垂直滚动条
		scrollY: 200px,
		scrollCollapse: true,
		paging: false
		
### 水平滚动条
		srcollX: true
		css样式中可以加入th,td{white-space: nowrap;}
		
### 复杂表头
		表头可以在html中的<th>标签中设置rowspan＝‘2’colspan＝‘2’ 这样来设置

### 初始化特定的表格
		$(document).ready(function() {
  			$('table.display').dataTable();
		} );
		
### 排序
	columnDefs: [ {
      targets: [ 0 ],
      orderData: [ 0, 1 ]  //如果第一列进行排序，有相同数据则按照第二列顺序排列
    }, {
      targets: [ 1 ],
      orderData: [ 1, 0 ]  //如果第二列进行排序，有相同数据则按照第一列顺序排列
    }, {
      targets: [ 4 ],
      orderData: [ 4, 0 ]  //如果第五列进行排序，有相同数据则按照第一列顺序排列
    } ]										

### 表格自适应
	html中添加width： 100%
	
### 国际化数字显示
	"language": {
     	"decimal":",",
       	"thousands":"."
    }
    
### 语言国际化
	"language": {
    	"lengthMenu": "每页 _MENU_ 条记录",
        "zeroRecords": "没有找到记录",
        "info": "第 _PAGE_ 页 ( 总共 _PAGES_ 页 )",
        "infoEmpty": "无记录",
        "infoFiltered": "(从 _MAX_ 条记录过滤)"
     }
     
### 隐藏列
    {
    	"targets": [ 2 ],
        "visible": false,
        "searchable": false
     }, 
     
### 默认排序
	"order": [[ 3, "desc" ]]
	
### 监听DataTables内置事件
	var eventFired = function(type) {
        var n = $('#demo_info')[0];
        n.innerHTML += '<div>' + type + ' 事件- ' + new Date().getTime() + '</div>';
        n.scrollTop = n.scrollHeight;
    }
	$('#example').on('order.dt',
    function() {
        eventFired('排序');
    })
    
### 点击行获取数据
	$(document).ready(function() {
    var table = $('#example').DataTable();
     
    $('#example tbody').on('click', 'tr', function () {
        var data = table.row( this ).data();
        alert( 'You clicked on '+data[0]+'\'s row' );
    } );
	} );            
	
### 列渲染
	"columnDefs": [{
    	"render": function(data, type, row) {
        	return data + ' (' + row[3] + ')';
        },
        "targets": 0
    }   		
    
### 行创建回调
	$(document).ready(function() {
    $('#example').dataTable( {
        "createdRow": function ( row, data, index ) {
            if ( data[5].replace(/[\$,]/g, '') * 1 > 4000 ) {
                $('td', row).eq(5).css('font-weight',"bold").css("color","red");
            }
        }
    } );
	} );
	
## 四种数据源
	1. ajax获取数据： 
	2. DOM作为数据源
	3. javascript数组
	4. 从服务器获取数据 ： 在服务器模式下，所有的分页，搜索，排序等操作，Datatables都会交给服务器去处理	    