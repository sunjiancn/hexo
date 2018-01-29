---
title: jqgrid使用说明
date: 2018-01-29 10:00:30
tags:
- jQuery
- table 
categories:
- 前端
---
# 介绍
    jqgrid是基于jQuery的表格插件。
[下载jqgrid](http://www.trirand.com/blog/?page_id=6)
# 用法
## 引用

```
<!-- jqGrid组件基础样式包-必要 -->
<link rel="stylesheet" href="jqgrid/css/ui.jqgrid.css" />

<!-- jqGrid主题包-非必要 --> 
<!-- 在jqgrid/css/css这个目录下还有其他的主题包，可以尝试更换看效果 -->
<link rel="stylesheet" href="jqgrid/css/css/redmond/jquery-ui-1.8.16.custom.css" />

<!-- jquery插件包-必要 -->
<!-- 这个是所有jquery插件的基础，首先第一个引入 -->
<script type="text/javascript" src="js/jquery-1.7.1.js"></script>

<!-- jqGrid插件包-必要 -->
<script type="text/javascript" src="jqgrid/js/jquery.jqGrid.src.js"></script>

<!-- jqGrid插件的多语言包-非必要 -->
<!-- 在jqgrid/js/i18n下还有其他的多语言包，可以尝试更换看效果 -->
<script type="text/javascript" src="jqgrid/js/i18n/grid.locale-cn.js"></script>
<title>http://blog.mn886.net/jqGrid</title>

<!-- 本页面初始化用到的js包，创建jqGrid的代码就在里面 -->
<script type="text/javascript" src="js/index.js"></script>
```
##  HTML

```
<table id="list2"></table> 
<div id="pager2"></div>
```
## JS

```
//创建jqGrid组件
	$("#list2").jqGrid(
			{
				url : 'data/JSONData.json',//组件创建完成之后请求数据的url
				datatype : "json",//请求数据返回的类型。可选json,xml,txt
				colNames : [ 'Inv No', 'Date', 'Client', 'Amount', 'Tax','Total', 'Notes' ],//jqGrid的列显示名字
				colModel : [ //jqGrid每一列的配置信息。包括名字，索引，宽度,对齐方式.....
				             {name : 'id',index : 'id',width : 55}, 
				             {name : 'invdate',index : 'invdate',width : 90}, 
				             {name : 'name',index : 'name asc, invdate',width : 100}, 
				             {name : 'amount',index : 'amount',width : 80,align : "right"}, 
				             {name : 'tax',index : 'tax',width : 80,align : "right"}, 
				             {name : 'total',index : 'total',width : 80,align : "right"}, 
				             {name : 'note',index : 'note',width : 150,sortable : false} 
				           ],
				rowNum : 10,//一页显示多少条
				rowList : [ 10, 20, 30 ],//可供用户选择一页显示多少条
				pager : '#pager2',//表格页脚的占位符(一般是div)的id
				sortname : 'id',//初始化的时候排序的字段
				sortorder : "desc",//排序方式,可选desc,asc
				mtype : "post",//向后台请求数据的ajax的类型。可选post,get
				viewrecords : true,
				caption : "JSON Example"//表格的标题名字
			});
	/*创建jqGrid的操作按钮容器*/
	/*可以控制界面上增删改查的按钮是否显示*/
	$("#list2").jqGrid('navGrid', '#pager2', {edit : false,add : false,del : false});
```
# 初始化参数

名称 | 类型 | 描述 | 默认值 | 可修改
---|---|---|---|---
url | string | 获取数据的地址|   |  
datatype | string | 从服务器端返回的数据类型，默认xml。可选类型：xml，local，json，jsonnp，script，xmlstring，jsonstring，clientside|  |  
mtype | string | ajax提交方式。POST或者GET，默认GET |   |
colNames | Array | 列显示名称，是一个数组对象| |
colModel | Array | 常用到的属性：name 列显示的名称；index 传到服务器端用来排序用的列名称；width 列宽度；align 对齐方式；sortable 是否可以排序| |
pager | string | 定义翻页用的导航栏，必须是有效的html元素。翻页工具栏可以放置在html页面任意位置| |
rowNum | int | 在grid上显示记录条数，这个参数是要被传递到后台| |
rowList | array | 一个下拉选择框，用来改变显示记录数，当选择时会覆盖rowNum参数传递到后台| |
sortname | string | 默认的排序列。可以是列名称或者是一个数字，这个参数会被提交到后台| |
viewrecords | boolean | 定义是否要显示总记录数| |
caption | string | 表格名称| |
[a1] | object | 对ajax参数进行全局设置，可以覆盖ajax事件 | null | 是
[a2] | object | 对ajax的select参数进行全局设置 | null | 是
altclass | string | 用来指定行显示的css，可以编辑自己的css文件，只有当altRows设为 ture时起作用 | ui-priority-secondary| 
altRows | boolean | 设置表格 zebra-striped 值| |
autoencode | boolean | 对url进行编码 | false | 是
autowidth | boolean | 如果为ture时，则当表格在首次被创建时会根据父元素比例重新调整表格宽度。如果父元素宽度改变，为了使表格宽度能够自动调整则需要实现函数：setGridWidth | false | 否
cellLayout | integer | 定义了单元格padding + border 宽度。通常不必修改此值。 | 5 | 是
cellEdit | boolean | 启用或者禁用单元格编辑功能 | false | 是
cellsubmit | string | 定义了单元格内容保存位置 | remote | 是
cellurl | string | 单元格提交的url | 空值 | 是
datastr | string | xmlstring或者jsonstring | 是
deselectAfterSort | boolean | 只有当datatype为local时起作用。当排序时不选择当前行 | true | 是
direction | string | 表格中文字的显示方向，从左向右（ltr）或者从右向左（rtr）| ltr | 否
editurl | string | 定义对form编辑时的url | 空值 | 是
emptyrecords | string | 当返回的数据行数为0时显示的信息。只有当属性 viewrecords 设置为ture时起作用	| | 是
ExpandColClick | boolean | 当为true时，点击展开行的文本时，treeGrid就能展开或者收缩，不仅仅是点击图片 | true | 否
ExpandColumn | string | 指定那列来展开tree grid，默认为第一列，只有在treeGrid为true时起作用 | 空值 | 否
[a3] | boolean | 当为true时，会在翻页栏之上增加一行	| false | 否
forceFit | boolean | 当为ture时，调整列宽度不会改变表格的宽度。当shrinkToFit 为false时，此属性会被忽略	| false | 否
gridstate | string | 定义当前表格的状态：'visible' or 'hidden'	| visible | 否
gridview | boolean | 构造一行数据后添加到grid中，如果设为true则是将整个表格的数据都构造完成后再添加到grid中，但treeGrid, subGrid, or afterInsertRow 不能用	| false | 是
height | mixed | 表格高度，可以是数字，像素值或者百分比	| 150 | 否
hiddengrid | boolean | 当为ture时，表格不会被显示，只显示表格的标题。只有当点击显示表格的那个按钮时才会去初始化表格数据。| false | 否
hidegrid | boolean | 启用或者禁用控制表格显示、隐藏的按钮，只有当caption 属性不为空时起效	| true | 否
hoverrows | boolean | 当为false时mouse hovering会被禁用	| false | 是
jsonReader | array | 描述json 数据格式的数组	| | 否
lastpage | integer | 只读属性，定义了总页数	| 0 | 否
lastsort | integer | 只读属性，定义了最后排序列的索引，从0开始	| 0	| 否
loadonce | boolean | 如果为ture则数据只从服务器端抓取一次，之后所有操作都是在客户端执行，翻页功能会被禁用	| false | 否
loadtext | string | 当请求或者排序时所显示的文字内容	| Loading....	| 否
loadui | string | 当执行ajax请求时要干什么。disable禁用ajax执行提示；enable默认，当执行ajax请求时的提示； block启用Loading提示，但是阻止其他操作	| enable | 是
multikey | string | 只有在multiselect设置为ture时起作用，定义使用那个key来做多选。shiftKey，altKey，ctrlKey	| 空值	| 是
multiboxonly | boolean | 只有当multiselect=true.起作用，当multiboxonly 为ture时只有选择checkbox才会起作用 | false | 是
multiselect|	boolean|	定义是否可以多选|	false|	否
multiselectWidth|	integer|	当multiselect为true时设置multiselect列宽度|	20|	否
page|	integer|	设置初始的页码|	1|	是
pagerpos|	string|	指定分页栏的位置|	center|	否
pgbuttons|	boolean|	是否显示翻页按钮|	true|	否
pginput|	boolean|	是否显示跳转页面的输入框|	true|	否
pgtext|	string|	当前页信息| 	| 	是
prmNames|	array|	Default valuesprmNames: {page:“page”,rows:“rows”, sort: “sidx”,order: “sord”, search:“_search”, nd:“nd”, npage:null} 当参数为null时不会被发到服务器端|	none|	是
postData|	array|	此数组内容直接赋值到url上，参数类型：{name1:value1…}|	空array|	是
reccount|	integer|	只读属性，定义了grid中确切的行数。通常情况下与records属性相同，但有一种情况例外，假如rowNum=15，但是从服务器端返回的记录数是20，那么records值是20，但reccount值仍然为15，而且表格中也只显示15条记录。|	0|	否
recordpos|	string|	定义了记录信息的位置： left, center, right|	right|	否
records|	integer|	只读属性，定义了返回的记录数|	none|	否
recordtext|	string|	显示记录数信息。{0} 为记录数开始，{1}为记录数结束。viewrecords为ture时才能起效，且总记录数大于0时才会显示此信| |
resizeclass|	string|	定义一个class到一个列上用来显示列宽度调整时的效果|	空值|	否
rowList|	array|	一个数组用来调整表格显示的记录数，此参数值会替代rowNum参数值传给服务器端。	|[]|	否
rownumbers|	boolean|	如果为ture则会在表格左边新增一列，显示行顺序号，从1开始递增。此列名为'rn'.|	false|	否
rownumWidth|	integer|	如果rownumbers为true，则可以设置column的宽度|	25|	否
savedRow|	array|	只读属性，只用在编辑模式下保存数据|	空值|	否
scroll|	boolean|	创建一个动态滚动的表格，当为true时，翻页栏被禁用，使用垂直滚动条加载数据，且在首次访问服务器端时将加载所有数据到客户端。当此参数为数字时，表格只控制可见的几行，所有数据都在这几行中加载|	false|	否
scrollOffset|	integer|	设置垂直滚动条宽度|	18|	否
scrollrows|	boolean|	当为true时让所选择的行可见|	false|	是
selarrrow|	array|	只读属性，用来存放当前选择的行|	array|	否
selrow|	string|	只读属性，最后选择行的id|	null|	否
shrinkToFit|	boolean|	此属性用来说明当初始化列宽度时候的计算类型，如果为ture，则按比例初始化列宽度。如果为false，则列宽度使用colModel指定的宽度|	true|	否
sortable|	boolean|	是否可排序|	false|	否
sortname|	string|	排序列的名称，此参数会被传到后台|	空字符串|	是
sortorder|	string|	排序顺序，升序或者降序（asc or desc）	|asc|	是
subGrid|	boolean|	是否使用suggrid|	false|	否
subGridModel|	array|	subgrid模型|	array|	否
subGridType|	mixed|	如果为空则使用表格的dataType|	null|	是
subGridWidth|	integer|	subgrid列的宽度|	20|	否
toolbar|	array|	表格的工具栏。数组中有两个值，第一个为是否启用，第二个指定工具栏位置（相对于body layer），如：[true,”both”] 。工具栏位置可选值：“top”,”bottom”, “both”. 如果工具栏在上面，则工具栏id为“t_”+表格id；如果在下面则为 “tb_”+表格id；如果只有一个工具栏则为 “t_”+表格id|	[false,'']|	否
totaltime|	integer|	只读属性，计算加载数据的时间。目前支持xml跟json数据|	0|	否
treedatatype|	mixed|	数据类型，通常情况下与datatype相同，不会变|	null|	否
treeGrid|	boolean|	启用或者禁用treegrid模式|	false|	否
treeGridModel|	string|	treeGrid所使用的方法|	Nested|	否
treeIcons|	array|	树的图标，默认值：{plus:'ui-icon-triangle-1-e',minus:'ui-icon-triangle-1-s',leaf:'ui-icon-radio-off'}|	 	|否
treeReader|	array|	扩展表格的colModel且加在colModel定义的后面|	 	|否
tree_root_level|	numeric|	root元素的级别|	0|	否
userData|	array|	从request中取得的一些用户信息|	array|	否
userDataOnFooter|	boolean|	当为true时把userData放到底部，用法：如果userData的值与colModel的值相同，那么此列就显示正确的值，如果不等那么此列就为空|	false|	是
viewrecords|	boolean|	是否要显示总记录数|	false|	否
viewsortcols|	array|	定义排序列的外观跟行为。数据格式：[false,'vertical',true].第一个参数是说，是否都要显示排序列的图标，false就是只显示 当前排序列的图标；第二个参数是指图标如何显示，vertical：排序图标垂直放置，horizontal：排序图标水平放置；第三个参数指单击功 能，true：单击列可排序，false：单击图标排序。说明：如果第三个参数为false则第一个参数必须为ture否则不能排序|	 	|否
width|	number|	如果设置则按此设置为主，如果没有设置则按colModel中定义的宽度计算	|none	|否
xmlReader	|array	|对xml数据结构的描述|	 	|否

# colModel 参数

属性 | 数据类型	| 备注| 默认值
---|---|---|---
align|	string|	left, center, right.|	left
classes|	string|	设置列的css。多个class之间用空格分隔，如：'class1 class2' 。表格默认的css属性是ui-ellipsis|	empty string
datefmt|	string|	”/”, ”-”, and ”.”都是有效的日期分隔符。y,Y,yyyy 年YY, yy 月m,mm for monthsd,dd 日.	|ISO Date (Y-m-d)
defval|	string|	查询字段的默认值|	空
editable|	boolean|	单元格是否可编辑|	false
editoptions|	array|	编辑的一系列选项。{name:’departmentid’,index:’departmentid’,width:200,editable:true,edittype:’select’,editoptions: {dataUrl:”/jqGrid/admin/deplistforstu.action”}},这个是演示动态从服务器端获取数据。	|empty
editrules|	array|	编辑的规则{name:’age’,index:’age’, width:90,editable:true,editrules: {edithidden:true,required:true,number:true,minValue:10,maxValue:100}},设定 年龄的最大值为100，最小值为10，而且为数字类型，并且为必输字段。	|empty
edittype|	string|	可以编辑的类型。可选值：text, textarea, select, checkbox, password, button, image and file.	|text
fixed|	boolean|	列宽度是否要固定不可变|	false
formoptions|	array|	对于form进行编辑时的属性设置|	empty
formatoptions|	array|	对某些列进行格式化的设置	|none
formatter|	mixed|	对列进行格式化时设置的函数名或者类型 {name:’sex’,index:’sex’, align:’center’,width:60,editable:true,edittype:’select’,editoptions: {value:’0:待定;1:男;2:女’},formatter:function(cellvalue, options, rowObject){return "";}},// 返回性别的图标。	|none
hidedlg|	boolean|	是否显示或者隐藏此列|	false
hidden|	boolean|	在初始化表格时是否要隐藏此列	|false
index|	string|	索引。其和后台交互的参数为sidx	|empty
jsonmap|	string|	定义了返回的json数据映射|	none
key|	boolean|	当从服务器端返回的数据中没有id时，将此作为唯一rowid使用只有一个列可以做这项设置。如果设置多于一个，那么只选取第一个，其他被忽略|	false
label|	string|	如果colNames为空则用此值来作为列的显示名称，如果都没有设置则使用name 值|	none
name|	string|	表格列的名称，所有关键字，保留字都不能作为名称使用包括subgrid, cb and rn.	|Required
resizable|	boolean|	是否可以被resizable|	true
search|	boolean|	在搜索模式下，定义此列是否可以作为搜索列	|true
searchoptions|	array|	设置搜索参数|	empty
sortable|	boolean|	是否可排序|	true
sorttype|	string|	用在当datatype为local时，定义搜索列的类型，可选值：int/integer - 对integer排序float/number/currency - 排序数字date - 排序日期text - 排序文本	|text
stype|	string|	定义搜索元素的类型| text
surl|	string|	搜索数据时的url|	empty
width|	number|	默认列的宽度，只能是象素值，不能是百分比|	150
xmlmap|	string|	定义当前列跟返回的xml数据之间的映射关系	|none
unformat|	function|	‘unformat’单元格值|	null

# 事件

事件 | 参数 | 备注
---|---|---
afterInsertRow|	rowidrowdatarowelem|	当插入每行时触发。rowid插入当前行的id；rowdata插入行的数据，格式为name: value，name为colModel中的名字
beforeRequest|	none|	向服务器端发起请求之前触发此事件但如果datatype是一个function时例外
beforeSelectRow|	rowid, e|	当用户点击当前行在未选择此行时触发。rowid：此行id；e：事件对象。返回值为ture或者false。如果返回true则选择完成，如果返回false则不会选择此行也不会触发其他事件
gridComplete|	none|	当表格所有数据都加载完成而且其他的处理也都完成时触发此事件，排序，翻页同样也会触发此事件
loadComplete|	xhr|	当从服务器返回响应时执行，xhr：XMLHttpRequest 对象
loadError|	xhr,status,error|	如果请求服务器失败则调用此方法。xhr：XMLHttpRequest 对象；satus：错误类型，字符串类型；error：exception对象
onCellSelect|	rowid,iCol,cellcontent,e|	当点击单元格时触发。rowid：当前行id；iCol：当前单元格索引；cellContent：当前单元格内容；e：event对象
ondblClickRow|	rowid,iRow,iCol,e|	双击行时触发。rowid：当前行id；iRow：当前行索引位置；iCol：当前单元格位置索引；e:event对象
onHeaderClick|	gridstate|	当点击显示/隐藏表格的那个按钮时触发；gridstate：表格状态，可选值：visible or hidden
onPaging|	pgButton|	点击翻页按钮填充数据之前触发此事件，同样当输入页码跳转页面时也会触发此事件
onRightClickRow|	rowid,iRow,iCol,e|	在行上右击鼠标时触发此事件。rowid：当前行id；iRow：当前行位置索引；iCol：当前单元格位置索引；e：event对象
onSelectAll|	aRowids,status|	multiselect为ture，且点击头部的checkbox时才会触发此事件。aRowids：所有选中行的id集合，为一个数组。status：boolean变量说明checkbox的选择状态，true选中false不选中。无论checkbox是否选择，aRowids始终有 值
onSelectRow|	rowid,status|	当选择行时触发此事件。rowid：当前行id；status：选择状态，当multiselect 为true时此参数才可用
onSortCol|	index,iCol,sortorder|	当点击排序列但是数据还未进行变化时触发此事件。index：name在colModel中位置索引；iCol：当前单元格位置索引；sortorder：排序状态：desc或者asc
resizeStart|	event, index|	当开始改变一个列宽度时触发此事件。event：event对象；index：当前列在colModel中位置索引
resizeStop|	newwidth, index|	当列宽度改变之后触发此事件。newwidth：列改变后的宽度；index：当前列在colModel中的位置索引
serializeGridData|	postData|	向服务器发起请求时会把数据进行序列化，用户自定义数据也可以被提交到服务器端


# 方法


```
jQuery("#grid_id").jqGrid('method', parameter1,...parameterN );
```


方法名 | 参数 | 返回值 | 说明
---|---|---|---
addJSONData|	data|	none|	使用传来的data数据填充表格。使用方法： var mygrid = jQuery(”#”+grid_id)[0]; var myjsongrid = eval(”(”+jsonresponse.responseText+”)”); mygrid.addJSONData(myjsongrid); myjsongrid = null; jsonresponse =null;
addRowData|	rowid,data, position, srcrowid|	成功为true, 否则为false|	根据参数插入一行新的数据，rowid为新行的id，data为新行的数据，position为新增行的位置，srcrowid为新增行的参考位置。data数据格式：{name1:value1,name2: value2…} name为在colModel中指定的名称
addXMLData|	data|	none|	根据传来的数据填充表格。用法：var mygrid = jQuery(”#”+grid_id)[0]; mygrid.addXmlData(xmlresponse.responseXML);
clearGridData|	clearfooter|	jqGrid对象|	清除表格当前加载的数据。如果clearfooter为true时则此方法删除表格最后一行的数据
delRowData|	rowid|	成功为true否则为false|	根据rowid删除行，但不会从服务器端删除数据
footerData|	action,data, format|	jgGrid对象|	设置或者取得底部数据。action：“get”或者“set”，默认为“get”，如果为“get”返回值为name:value，name为colModel中名称。如果为“set”则值为name：value，name是colModel中的名称。format：默认为true，当为 true时，在设置新值时会调用formatter格式化数值
getCell|	rowid, iCol|	单元格内容|	返回指定rowid，iCol的单元格内容，iCol既可以是当前列在colModel中的位置索引也可以是name值。注意：在编辑行或者单元格时不能使用此方法，此时返回的并不是改变的值，而是原始值
getCol|	colname, returntype, mathoperation|	array[] or value	|返回列的值。colname既可以是当前列在colModel中的位置索引也可以是name值。returntype指定返回数据的类型，默认为false。当为false时，返回的数组中只包含列的值，当为true时返回数组是对象数组，具体格式 {id:rowid, value:cellvalue} ，id为行的id，value为列的值。如： [{id:1,value:1},{id:2,value:2}…]。mathoperation 可选值为'sum, 'avg', 'count'
getDataIDs|	none|	array[]|	返回当前grid里所有数据的id
getGridParam|	name|	mixed value|	返回请求的参数信息
getInd|	rowid,rowcontent|	mixed|	如果rowcontent为false，返回行所在的索引位置，id为行id。rowcontent默认为false。如果rowconent为ture则返回的为行对象，如果找不到行则返回false
getRowData|	rowid or none|	array[]|	返回指定行的数据，返回数据类型为name:value，name为colModel中的名称，value为所在行的列的值，如果根据rowid找不到则返回空。在编辑模式下不能用此方法来获取数据，它得到的并不是编辑后的值
hideCol|	colnameor[colnames]|	jqGrid对象|	如果参数为一个列名则隐藏此列，如果给定的是数组则隐藏指定的所有列。格式： [“name1”,”name2”]
remapColumns|	permutation, updateCells, keepHeader|	none|	调整表格列的显示顺序,permutation为当前列的顺序，假如值是[1,0,2]，那么第一列就会在第二位显示。如果updateCells为ture则是对单元格数据进行重新排序，如果keepHeader为true则对header数据显示位置进行调整
resetSelection|	none|	jqGrid对象|	选择或者反选行数据，在多选模式下也同样起作用
setCaption|	caption|	jqGrid对象|	设置表格的标题
setCell|	rowid,colname, data, class, properties|	jqGrid对象|	改变单元格的值。rowid：当前行id；colname：列名称，也可以是列的位置索引，从0开始；data：改变单元格的内容，如果为空则不更 新；class：如果是string则会使用addClass方法将其加入到单元格的css中，如果是array则会直接加到style属性中；properties：设置单元格属性
setGridParam|	object|	jqGrid对象|	设置grid的参数。有些参数的修改必须要重新加载grid才可以生效，这个方法可以覆盖事件
setGridHeight|	newheight|	jqGrid对象|	动态改变grid的高度，只能对单元格的高度进行设置而不能对表格的高度进行动态修改。new_height：可以是象素值，百分比或者"auto"
setGridWidth|	newwidth,shrink|	jqGrid对象|	动态改变表格的宽度。newwidth:表格宽度，象素值；shrink：true或者false，作用同shrinkToFit
setLabel|	colname, data, class, properties|	jqGrid对象|	给指定列设置一个新的显示名称。colname：列名称，也可以是列的位置索引，从0开始；data：列显示名称，如果为空则不修改；class：如果是 string则会使用addClass方法将其加入到单元格的css中，如果是array则会直接加到style属性中；properties：设置 label的属性
setRowData|	rowid,data, cssprop|	成功true否则false|	更新行的值，rowid为行id。data值格式：{name1:value1,name2: value2…} name为colModel中名称；cssprop：如果是string则会使用addClass方法将其加入到行的css中，如果是array或者对象 则会直接加到style属性中
setSelection|	rowid,onselectrow|	jqGrid对象|	选择或反选指定行。如果onselectrow为ture则会触发事件onSelectRow，onselectrow默认为ture
showCol|	colname|	jqGrid|	显示列。colname可以是数组[“name1”,”name2”],但是name1或者name2必须是colModel中的name
trigger(“reloadGrid”)|	none|	jqGrid对象|	重新加载当前表格，也会向服务器发起新的请求
updateColumns|	none|	none|	同步表格的宽度，用在表格拖拽时，用法：var mygrid=jQuery(”#grid_id”)[0];mygrid.updateColumns();

