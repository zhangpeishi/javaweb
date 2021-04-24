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









​	



 

