# 可视化配置__加载器
- 功能：可以通过可视化界面进行配置的输入，并导出成多种配置文件。

# 使用
1. 编写XML文件
XML文件基本格式如下
<?xml version="1.0" encoding="utf-8"?>
<windows title="" height="" widht="">
	<row key="">
	</row>
</windows>

其中windos节点是根节点，使用**title**表示输出后**文件的名称**，**height和weight**表示可视化界面的**高度和宽度**。
row是表示一类配置，其中**key属性**会转化为**ini文件中的Seciton**。
出来两个两个基础节点，通过以下节点实现配置输入。

>1. 文本输入（text）
```xml
<text key="DefEncodingNoFound" label_name="文本框"></text>
```
>2. 单选（radio）
```xml
<radio key="CacheSitePage" label_name="单选按钮">Y(true)|N(false)</radio>
```
>3. 多选框（checkbox）
```xml
<checkbox key="DefPageSuffix" label_name="多选框">C1(cb1)|C2(cb2)|C3(cb3)</checkbox>	
```
>4. 下拉框（select）
```xml
<select key="NumThread" label_name="下拉框">1|2|4|8|16|32|64</select>
```

>上述，key属性会转化为ini文件中键（Key），你做的配置会保存为对应键（Key）的值（Value），label_name属性是，可视化界面的该项目的输入提示
text节点的值为空（不用编辑），其他节点如果有多个选项，使用|分割，并且如果选项后带有小括号（英文），则在保存数据时，保存对于的小括号中的值

>例如，给定的demo.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<windows title="演示配置" height="550" widht="500">
<row key="Request">
	<select key="UA" label_name="UA选择">随机生成(1)|来源于文件(2)</select>
</row>
<row key="Coding">
	<checkbox key="DefEncoding" label_name="默认使用编码">utf-8|big5|gbk</checkbox>
	<text key="DefEncodingNoFound" label_name="编码不确定，强制使用"></text>
</row>
<row key="SavePage">
	<radio key="CacheSitePage" label_name="是否缓存网页">缓存(true)|不缓存(false)</radio>
	<checkbox key="DefPageSuffix" label_name="允许缓存的网页后缀">html|htm|asp|shtml|php|jsp|nsp|sp</checkbox>
</row>
<row key="LoadFunc">
	<radio key="UseStatic" label_name="静态请求">静态请求(true)|动态请求(false)</radio>
	<select key="NumThread" label_name="请求线程数量">1|2|4|8|16|32|64l</select>
</row>
</windows>
```

2. 运行程序

安装，并运行程序。
3. 输入配置

**配置中不能含有空、未选选择的属性，否者无法保存。**
4. 保存并导出

目前支持导出文件类型（**xml,ini,json**,csv）。
5. 导出文件示例

>1.**Json**
```json
{
"Request": {
"UA": 2.0
},
"Coding": {
"DefEncoding": [
    "utf-8",
    "big5"
],
"DefEncodingNoFound": "utf-8"
},
"SavePage": {
"CacheSitePage": true,
"DefPageSuffix": [
    "html",
    "htm",
    "asp"
]
},
"LoadFunc": {
"UseStatic": true,
"NumThread": 4.0
}
}
```
>2.**XMl**
```xml
<root type="object">
<Request type="object">
	<UA type="number">
		2.0
	</UA>
</Request>
<Coding type="object">
	<DefEncoding type="array">
		<item type="string">
			utf-8
		</item>
		<item type="string">
			big5
		</item>
	</DefEncoding>
	<DefEncodingNoFound type="string">
		utf-8
	</DefEncodingNoFound>
</Coding>
<SavePage type="object">
	<CacheSitePage type="boolean">
		true
	</CacheSitePage>
	<DefPageSuffix type="array">
		<item type="string">
			html
		</item>
		<item type="string">
			htm
		</item>
		<item type="string">
			asp
		</item>
	</DefPageSuffix>
</SavePage>
<LoadFunc type="object">
	<UseStatic type="boolean">
		true
	</UseStatic>
	<NumThread type="number">
		4.0
	</NumThread>
</LoadFunc>
</root>
```
>3.**Ini**(这是ini文件类型)
```
[Request]
UA=	2.0
[Coding]
DefEncoding=	[utf-8,big5]
DefEncodingNoFound=	utf-8
[SavePage]
CacheSitePage=	true
DefPageSuffix=	[html,htm,asp]
[LoadFunc]
UseStatic=	true
NumThread=	4.0
```
>4.csv（csv类型）
```
Request,UA,2.0
Coding,DefEncoding,utf-8,big5
Coding,DefEncodingNoFound,utf-8
SavePage,CacheSitePage,true
SavePage,DefPageSuffix,html,htm,asp
LoadFunc,UseStatic,true
LoadFunc,NumThread,4.0
```






















