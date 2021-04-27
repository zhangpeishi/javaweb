## jQuery

使用jQuery一定要引入jQuery库，$是一个函数 $(function(){	}); 相当于window.onload = funtion(){}

### jQuery的核心函数 $

dom对象 ： [obj HTMLxxxElement]

jquery对象：[object Object]

### jquery 的本质

jquery对象的本质是dom对象的数组 + jQuery 提供的一系列函数

### 两者的使用区别：

​	dom不能使用jQuery的属性和方法，jQuery也不能使用dom 的属性和方法

### 两者的相互转换

dom-jquery

$(dom)

Jquery-dom 

取下标即可

标签

### 基础选择器

#ID .class 标签名 *

### 层级选择器 

Body 里面的的所有div$("body div")

body里面的儿子div $("body>div") 下一层的

ID为one的下一个div $("#one+div") 同层后面一个



ID为two的元素后面的所有div$("#two~div")同层后面所有

### 过滤选择器

1. 基本 :first :last :not(selector) :even :odd :eq(index):gt(index)大于index  :lt(index)小于index :header所有的标题标签:animated 所有正在执行动画的标签

2. 内容：:contains(txt) :empty :has(selector):parent非空

3. 属性过滤选择器：[attribute] 例如：$("div[id]") 选择有id属性的div元素 [attribute=value] $("div[name = 'ztt']") 选择所有name属性为ztt的div元素

4. 表单过滤器：:input :text :password :radio :checkbox :submit :image:reset :button :file :hidden

   $(":text:disabled").val("")

   $(":checkbox:disabled").val("")

   Val()方法可以操作表单项的值 文本框 单选框 复选框 下拉列表框

   #### 获取所有选中的复选框的值

   1. 获取全部选中的复选框标签对象$(":checkbox:checked")

   2. 遍历 取到每一个dom对象 使用dom对象的value属性

      var $checkboxes = $(":checkbox:checked")

      ​	for(var i =0;i<$checkboxes;i++){

      ​		alert($checkboxes[i].value);

      }

      ### each 是jQuery对象用来遍历元素的方法

      $checkboxes.each(function(){

      ​	alert($checkboxes[i].value)

      }); 简化成

      $checkboxes.each(function(){

      ​	alert(this.value)

      }); this 表示当前遍历到的dom对象

      #### 获取下拉框选中的内容

      1. 获取选中的option标签对象

         var $options = $("select option:selected");

      2. 遍历，获取option便签中的文本内容

         $options.each(function(){						//在each遍历的function函数中，有一个this对象，这个this对象是当前正在遍历到的dom对象

         ​	alert(this.innerHTML);

         })

   ![image-20210424182455951](/Users/zhangpeishi/IdeaProjects/javaweb/messages/image-20210424182455951.png)

   

   ![image-20210424184205441](/Users/zhangpeishi/IdeaProjects/javaweb/messages/image-20210424184205441.png)

   



### jQuery 的属性操作

​	

1. html() 可以设置和获取起始标签和结束标签中间的内容 和dom对象的属性innerHTML一样

2. text() 可以设置和获取起始标签和结束标签中间的文本和dom对象的属性innerText一样

3. val() 可以设置和获取表单项的value属性值 和dom对象属性value 一样

   

批量操作单选和多选框

:radio :checkbox 是选择imput 标签中type是radio 和CheckBox的

$(":radio").val(["radio2"])

$(":checkbox").val(["checkbox1","checkbox2","checkbox3"])

操作下拉选择框：

$("#multiple").val(["mul1,mul2"]);
<select id="multiple" multiple = ”multiple" size = 4>
  <option value = 'mul1'>mul1</option>
  <option value = 'mul2'>mul2</option>
  <option value = 'mul3'>mul3</option>                                 
  <option value = 'mul4'>mul4</option>                                 
</select>



$(":radio").val(["radio2"])

一次性选中所有的

![image-20210424200847039](/Users/zhangpeishi/IdeaProjects/javaweb/messages/image-20210424200847039.png)



attr() 可以设置和获取属性的值，不推荐操作checked,readOnly selected,disabled等

prop()可以设置和获取属性的值 只推荐操作checked,readOnly selected,disabled等



### Dom的增删改

内部插入	a.appendTo(b) 把a插入到b子元素末尾，成为最后一个子元素

​					a.prependTo(b)把a插到b所以子元素前面，成为第一个子元素

外部插入	a.insertAfter(b)把a插入到b的后面	a.insertBefore(b) 把a插入到b的前面

替换	a.replaceWith(b) 用b替换a 所有的替换成一个 a.replaceAll(b) 用a替换掉所有的b

删除	remove()  a.remove()删除a标签 a.empty()把a标签里的内容删除

例如：动态添加删除表格内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="https://libs.baidu.com/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript">
        $(function () {
            $("#addEmpbutton").click(function () {

                var $name = $("#empname").val();
                var $email = $("#empemail").val();
                var $salary = $("#empsalary").val();

                var $obj = $("<tr>\n" +
                    "            <td>"+$name+"</td>\n" +
                    "            <td>"+$email+"</td>\n" +
                    "            <td>"+$salary+"</td>\n" +
                    "            <td><a href=\"deleteEmpid-003\">Delete</a></td>\n" +
                    "        </tr>");
                $obj.appendTo("#employeetable");

            }
            );
            $("a").click(function () {
                
                
                $obj = $(this).parent().parent();
                if(confirm("确定要删除吗？")){
                    $obj.remove();
                    

                }


                return false;//阻止标签跳转
            });

        });
    </script>
</head>
<body>
<div id="div4">

    <table id="employeetable" border="1">
        <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Salary</th>
            <th>

            </th>
        </tr>
        <tr>
            <td>Tom</td>
            <td>tom@tom.com</td>
            <td>8000</td>
            <td> <a href="deleteEmpid-001">Delete</a></td>
        </tr>
        <tr>
            <td>Jerry</td>
            <td>jerry@jerry.com</td>
            <td>12000</td>
            <td><a href="deleteEmpid-002">Delete</a></td>
        </tr>
        <tr>
            <td>Bob</td>
            <td>bob@bob.com</td>
            <td>13000</td>
            <td><a href="deleteEmpid-003">Delete</a></td>
        </tr>




    </table>


</div>
<div id="div-1">
    <h4>添加新员工</h4>
    <table>
        <tr>
            <td class="inp">name:</td>
            <td><input type="text" id="empname" name="empname"/></td>
        </tr>
        <tr>
            <td class="inp">email:</td>
            <td><input type="text" id="empemail" name="empemail"/></td>
        </tr>
        <tr>
            <td class="inp">salary:</td>
            <td><input type="text" id="empsalary" name="empsalary"/></td>
        </tr>
        <tr>
            <td colspan="2" align="center">
                <button id="addEmpbutton" value="abc">submit</button>
            </td>
        </tr>
    </table>

</div>

</body>
</html>
```



### jQuery的动画操作

1. 基本动画 show() 将隐藏的文件显示hide()将显示的文件隐藏 toggle()显示的文件隐藏，隐藏的显示 有两个参数，第一个参数是动画的时间，以毫秒为单位，第 二个参数是回调函数 表示动画完成之后的执行

2. 淡入淡出动画

   



### jQuery事件处理方法

![image-20210426152546269](/Users/zhangpeishi/IdeaProjects/javaweb/messages/image-20210426152546269.png)

​	

### 事件冒泡

父子元素同时绑定一个事件，当子元素触发，父元素也触发

 ![image-20210426152907068](/Users/zhangpeishi/IdeaProjects/javaweb/messages/image-20210426152907068.png)

在子元素里面return false即可

JavaScript事件对象

事件对象，是封装有触发事件信息的一个JavaScript对象 我们重点关心怎么拿到这个JavaScript的事件对象以及使用。

获取JavaScript事件

jQuery 获取事件对象

$("#areaDiv").click(function(event){

Console.log("");

});

$("#areaDiv").bind("mouseover mouseout",function(){

if(event.type =  'mouseover'){

Console.log("");

}

});

![image-20210426204413821](/Users/zhangpeishi/IdeaProjects/javaweb/messages/image-20210426204413821.png)

# xml

## xml语法

1. 文档声明
2. 元素（标签）
3. xml属性
4. xml注释
5. 文本区域（CDATA区)

## 使用dom4j解析xml

 ### 1.配置dom4j

​	web-inf 下面 lib中传入jar包

### 2.获取document对象

​	

```xml
//1.读取xml文件，获取document对象
SAXReader reader  = new SAXReader();
Document document  = reader.read(new File(""));
//2.读取xml形式的文本，得到document对象
String text = "<csdn></csdn>";
Document document = DocumentHelper.parseText(text);
//3.主动创建Document对象
Document document = DocumentHelper.createDocument();
Element root = document.addElement("csdn");//创建根节点
```



### 3.节点对象操作方法

```xml
//1.获取文档的根节点
Element root = document.getRootElement();
//2.取得某个节点的子节点
Element element = node.getElement("四大名著");
//3.取得节点的文字
String text = node.getText();
//4.取得某节点下名为“CSDN”的子节点，并遍历
List nodes = rootElm.getElements("CSDN");
for(Iterator it = nodes.iterator();it.hasNext();){
	Element element = (Element)it.next();
	//do something
}
//5.对根节点下的所有子节点进行遍历
for(Iterator it = root.elementIterator();it.hasNext();){
		Element element = (Element)it.next();
	//do something
}
//6.在某节点下添加子节点
Element element = node.addElement("朝代");
//7.设置节点文字
element.setText("明朝")；
//8.删除某节点
//childElement是待删除的节点,parentElement是其父节点  
parentElement.remove(childElment);
//9.添加一个CDATA节点
Element e = infoElement.addElement("content");
e.addCDTA("CDATA区域");
```



### 4.节点对象的属性操作方法

```xml
//1.取得某节点下的某属性
Element root = Document.getRootElement();
Attribute attribute = root.attribute("id");
//2.取得属性的文字
String text = attribute.getText();
//3.删除某属性
Attribute attribute = root.attribute("size");
root.remove(attribute);
//4.遍历某节点的所有属性
Element root = document.getRootElement();
for(Iterator it = root.attributeIterator();it.hasIterator();){
	Attribute attribute = (Attribute)it.hasNext();
	//do something
}
//5.设置某节点的文字和属性
element.addAttribute("name","zhangtingting");
//6.设置属性的文字
Attribute attribute = root.attribute("name"); attribute.setText("zhangtingting");
```



### 5.将文档写入xml文件

```xml
//1.文档中全为英文，不设置编码，直接写入
XMLWriter writer = new XMLWriter(new FileWriter("test.xml"));
writer.write(document);
writer.close();
//2.文档中含有中文，设置编码格式
OutputFormat format = OutputFormat.createPrettyPrint();
format.setEcoding("UTF-8");
XMLWriter writer = new XMLWriter(new FileWriter("output.xml"),format);
writer.write(document);
writer.close();
```



### 6.字符串与xml转换

```
1.将字符串转化为XML
      String text = "<csdn> <java>Java班</java></csdn>";
      Document document = DocumentHelper.parseText(text);
2.将文档或节点的XML转化为字符串.
       SAXReader reader = new SAXReader();
       Document   document = reader.read(new File("csdn.xml"));            
       Element root=document.getRootElement();    
       String docXmlText=document.asXML();
       String rootXmlText=root.asXML();
       Element memberElm=root.element("csdn");
       String memberXmlText=memberElm.asXML();
```

### 练习

https://blog.csdn.net/redarmy_chen/article/details/12969219

# 部署javaweb到Tomcat的两种方法



 [javaweb项目环境配置.pdf](../../Desktop/javaweb项目环境配置.pdf) 



