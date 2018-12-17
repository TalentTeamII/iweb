# iweb
平台二组前端常见问题征集平台，帮助大家少采坑。




### 1.jQuery prop和attr
#### 问题背景:
	使用attr 无法设置/获取状态 checked disable等状态。
	
#### 案例代码

```javascript
$( elem ).attr("checked")
$( elem ).attr("checked",true)
```
#### 问题原因
在jQuery1.6之前和之后api变化,比如，selectedIndex, tagName, nodeName, nodeType, ownerDocument, defaultChecked, 和defaultSelected应该使用.prop()方法获取/设置值。 在jQuery1.6之前这些不属于attribute的property需要用.attr()方法获取。这几个并没有相应的attibute，只有property。

#### 解决思路

其实明白了上面讲的内容，什么时候该使用.attr()什么时候该使用 .prop()就很清楚了，不过还是传一张坊间很流行的图
![](https://images0.cnblogs.com/blog/349217/201310/01161410-90dde52753e040f3a09b83c418e94026.png)




### 2.jQuery trim()
#### 问题背景:
jQuery的trim()在某些IE报错或不兼容问题

#### 案例代码

```

<form action="" method="post">
        用户名：<input type="text" id="userid" value="teamii" />
</form>
//trim（）方法，去除字符串空格
var n=$("#userid").val().trim();
alert(n)


```
####解决思路 &
可以使用以下解决方案

一、使用 $.trim(username)或者jQuery.trim(name)才是正确的用法。<br/>
二、重写js原生String 添加trim方法

```javascript
 String.prototype.trim = function()  
 {  
      return this.replace(/(^\s*)|(\s*$)/g, "");  
 }
 
 username=$("#username").val().toString().trim();
 这里注意 如果使用jquery获取值 使用toString转换为普通的js对象 才能进行trim
 
```

### 3.jQuery remove()
#### 问题背景:
ie11浏览器发现jq的remove方法总是报错， jquery SCRIPT5007: 缺少对象

#### 解决思路
先找要删除的节点的父级节点,然后使用原生js的removeChild方法删除该节点。

```

 var ele = document.getElementById("要删除的节点id");
document.getElementById("要删除节点的父节点id").removeChild(ele);


//ele必须是js对象，也可以把jq对象转换成js对象，
//用document.getElementById(),必须有id才可以，局限性大  使用jq选择器获取到对象之后再转js对象
var ele =$(".class")[0];//  jq转js对象
$('.class_parent')[0].removeChild(ele);


```
