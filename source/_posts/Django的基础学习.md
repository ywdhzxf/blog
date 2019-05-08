
---
title: Django的基础学习
date: 2019-05-06 12:36:15
tags: web前端
---


## 搭建Django框架

### 1 基本搭建

```
1 创建一个文件夹
	mkdir mytest
2 在文件夹里面创建一个项目
	Django-admin startproject mysite
3 在里面创建一个应用 
	python3.6 manage.py startapp myweb
```

### 2 执行数据库连接配置

```
1 编辑init文件,添加Pymysql的数据库
		import pymysql
		pymysql.install_as_MySQLdb()
	
2 进入setting配置文件,进行修改
	INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'mytest',    #写上创建的应用名
]
	DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.mysql',
          'NAME': 'mydb',   #写上库名
          'USER': 'root',
          'PASSWORD': '123456',
          'HOST': 'localhost',
          'PORT': '3306',
}
	#此处添加自己的IP地址
    ALLOWED_HOSTS = ['192.168.2.240']
```

### 3 配置路由

```
1 配置主路由(第一层路径正则筛选)
	from django.conf.urls import include,url
	from django.contrib import admin

    urlpatterns = [
        url(r'^admin/', admin.site.urls),
        url(r'^mytest/', include('mytest.urls')),
    ]
2 配置应用路由(第二层路径筛选)(必须要有相对应的视图)
	from django.conf.urls import url
	from . import views

    urlpatterns = [
        url(r'^$', views.index, name="index"),
    ]
```

### 4 编写相对应的视图

```
写相对于应用路由的视图
from django.shortcuts import render
from django.http import HttpResponse

from mytest.models import Users

def index(request):      ###命名一定是路由的命名
    try:
        s = Users.objects.get(id=1)
        return HttpResponse(s)
    except:
        return HttpResponse("没有找到对应的信息！")
```

### 5 测试

```
python3.6 manage.py sunserver 0:8000
```

## 数据库的增删改查

### 1 视图

```
视图的填写

from django.shortcuts import render
from django.http import HttpResponse,HttpResponseRedirect
from django.core.urlresolvers import reverse
from django.shortcuts import redirect

from mytest.models import Users

def index(request):
    try:
        list = Users.objects.filter(id__in=[1,3,5])
        s = ','.join([vo.name for vo in list])
        
        #修改(将id值为5的age值改为30)
        #ob = Users.objects.get(id=5)
        #ob.age = 30
        #ob.save()

        #删除(删除id为3的信息)	
        #ob = Users.objects.get(id=3)
        #ob.delete()
        
        return HttpResponse(s)
    except:
        return HttpResponse("没有找到对应的信息！")

# 浏览用户信息        
def indexUsers(request):
    # 执行数据查询，并放置到模板中
    list = Users.objects.all()
    context = {"stulist":list}
    return render(request,"mytest/users/index.html",context)

# 加载添加信息表单
def addUsers(request):  
    return render(request,"mytest/users/add.html")

# 执行信息添加操作
def insertUsers(request): 
    try:
        ob = Users()
        ob.name = request.POST['name']
        ob.age = request.POST['age']
        ob.phone = request.POST['phone']
        ob.save()
        context = {'info':'添加成功！'}
    except:
        context = {'info':'添加失败！'}
    return render(request,"mytest/users/info.html",context)

# 执行信息删除操作    
def delUsers(request,uid):  
    try:
        ob = Users.objects.get(id=uid)
        ob.delete()
        #重定向到信息浏览页
        return HttpResponseRedirect(reverse("users"))
        #同上重定向跳转的简写 return redirect(reverse("users"))
    except:
        context = {'info':'删除失败！'}
        return render(request,"mytest/users/info.html",context)

# 加载信息编辑表单    
def editUsers(request,uid):  
    try:
        ob = Users.objects.get(id=uid)
        context = {'user':ob}
        return render(request,"mytest/users/edit.html",context)
    except:
        context = {'info':'没有找到要修改的信息！'}
        return render(request,"mytest/users/info.html",context)

# 执行信息编辑操作
def usersupdate(request,uid):
    try:
        ob = Users.objects.get(id=uid)
        ob.username = request.POST['username']
        ob.name = request.POST['name']
        ob.passwd = request.POST['passwd']
        ob.sex = request.POST['sex']
        ob.address = request.POST['address']
        ob.code = request.POST['code']
        ob.phone = request.POST['phone']
        ob.email = request.POST['email']
        ob.state = request.POST['state']
        ob.addtime = time.time()
        ob.save()
        context = {'info':'修改成功'}
    except:
        context = {'info':'修改失败'}
    return render(request,'myadmin/info.html',context)
    
```

### 2 html

#### 主页

```


<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8"/>
        <title>用户信息管理</title>
        <script>
            //自定义执行信息删除提示判断，参数uu是成功的删除url地址
            function doDel(uu){
                if(confirm("确定要删除吗？")){
                    //网页跳转
                    window.location=uu;
                }
            }

        </script>
    </head>
    <body>
        <center>

            {% include 'mytest/users/menu.html' %}

            <h3>浏览用户信息</h3>
            <table width="800" border="1">
                <tr>
                    <th>id号</th>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>电话</th>
                    <th>操作</th>
                </tr>
                {% for stu in stulist %}
                    <tr>
                        <td>{{ stu.id }}</td>
                        <td>{{ stu.name }}</td>
                        <td>{{ stu.age }}</td>
                        <td>{{ stu.phone }}</td>
                        <td>
                            <a href="{% url 'editusers' stu.id %}">编辑</a>
                            <a href="javascript:doDel('{% url 'delusers' stu.id %}');">删除</a>
                        </td>
                    </tr>
                {% endfor %}
            </table>
        </center>
    </body>
</html>
```

#### 添加

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8"/>
        <title>用户信息管理</title>
    </head>
    <body>
        <center>
            {% include "mytest/users/menu.html" %}

            <h3>添加用户信息</h3>
            <form action="{% url 'insertusers' %}" method="post">
            {% csrf_token %}
            <table width="280" border="0">
               <tr>
                 <td>姓名：</td>
                 <td><input type="text" name="name"/></td>
               </tr>
               <tr>
                 <td>年龄：</td>
                 <td><input type="text" name="age"/></td>
               </tr>
               <tr>
                 <td>电话：</td>
                 <td><input type="text" name="phone"/></td>
               </tr>
               <tr>
                 <td colspan="2" align="center">
                    <input type="submit" value="添加"/>
                    <input type="reset" value="重置"/>
                 </td>
               </tr>
            </table>
            </form>
        </center>
    </body>
</html>
```

#### 修改

```
{% extends "myadmin/base.html" %}

 
{%block block_name%}
<!-- 主体开始 -->

	<h1>
		Edit Your Profile
	</h1>
	<form id="edit-profile" class="form-horizontal" action="{% url 'myadmin_usersupdate' user.id %}" enctype="multipart/form-data" method="post">
	{% csrf_token %}
		<fieldset>
			<legend>编辑用户信息</legend>
			<div class="control-group">
				<label class="control-label" for="input01">username</label>
				<div class="controls">
					<input type="text" class="input-xlarge" id="input01" name='username' value='{{ user.username }}'/>
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">name</label>
				<div class="controls">
					<input type="passwo" class="input-xlarge" id="input01" name='name' value='{{ user.name }}'/>
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">passwd</label>
				<div class="controls">
					<input type="text" class="input-xlarge" id="input01" name='passwd' value='{{ user.passwd }}'/>
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">sex</label>
				<div class="controls">
					&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
					<input type="radio" name='sex' value="1" />男
					&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
					<input type="radio" name='sex' value="0" />女
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">address</label>
				<div class="controls">
					<input type="text" class="input-xlarge" id="input01" name='address' value='{{ user.address }}'/>
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">code</label>
				<div class="controls">
					<input type="text" class="input-xlarge" id="input01" name='code' value='{{ user.code }}'/>
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">phone</label>
				<div class="controls">
					<input type="text" class="input-xlarge" id="input01" name='phone' value='{{ user.phone }}'/>
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">email</label>
				<div class="controls">
					<input type="text" class="input-xlarge" id="input01" name='email' value='{{ user.email }}'/>
					
				</div>
			</div>
			<div class="control-group">
				<label class="control-label" for="input01">state</label>
				<div class="controls">
					&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
					<input type="radio" name="state" value="1" />启用
					&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
					<input type="radio" name="state" value="2" />禁用
					&nbsp;&nbsp;&nbsp;&nbsp;
					<input type="radio" name="state" value="0" />后台管理员
				</div>
			</div>
			
			<!-- <div class="control-group">
				<label class="control-label" for="fileInput">Photo</label>
				<div class="controls">
					<input class="input-file" id="fileInput" type="file" />
				</div>
			</div>						
			<div class="control-group">
				<label class="control-label" for="textarea">Biography</label>
				<div class="controls">
					<textarea class="input-xlarge" id="textarea" rows="4">Web technology junkie who writes innovative and bestselling technical books. Also enjoys Sunday bicycle rides and all "good" comedy.</textarea>
				</div>
			</div> -->
									
			<div class="form-actions">
				<button type="submit" class="btn btn-primary">Save</button> <button class="btn">Cancel</button>
			</div>
		</fieldset>
	</form>

<!-- 主体结束 -->
{%endblock%}

```

#### info显示

```
  menu
  <h2>用户信息管理</h2>
        <a href="{% url 'users' %}">浏览用户</a> |
        <a href="{% url 'addusers' %}">添加用户</a>
        <hr/>
```

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8"/>
        <title>用户信息管理</title>
    </head>
    <body>
        <center>
            {% include "mytest/users/menu.html" %}

            <h3>{{ info }}</h3>

        </center>
    </body>
</html>
```

## 静态文件

### 1 注意

```
1 修改setting里面的静态设定(在最后)
	STATIC_URL = '/static/'
	STATICFILES_DIRS = [
    	os.path.join(BASE_DIR, 'static'),
	]

2 在每一个页面都使用编码(每个页面前都必须要加)
	{% load static from staticfiles %}
```

### 2 使用方法

```
创建一个base.html,base是父,其他为子,所有的公共部分都放在父文件里以便调用
{% csrf_token %}
1 占位标签
	{%block block_name%}
	这里可以定义默认值
	如果不定义默认值，则表示空字符串
	{%endblock%}
	在base文件中任意位置可以占位,然后可以在子文件中写上占位标签就可以自己定义那块部分的内容,注意标签名字不能重复
	
2 继承标签
	{% extends "base.html" %}
在子文件中写入继承标签就可以继承父类里面的公共信息
```

### 提交表单注意

```
from 里面需要写
	action="{% url 'myadmin_usersinsert' %}" 					enctype="multipart/form-data" method="post"
	
下面需要加
{% csrf_token %}
```

## 分页

```
# stu信息分页实例
    url(r'^stu/(?P<pIndex>[0-9]*)/$', views.stu, name='stu'),
```

```
#stu学生信息分页实例
def stu(request,pIndex):
    #return HttpResponse('ok')
    list = Stu.objects.filter()
    #实例化分页对象
    p = Paginator(list,5)
    # 处理当前页号信息
    if pIndex=="":
        pIndex = '1'
    pIndex = int(pIndex)
    # 获取当前页数据
    list2 = p.page(pIndex)
    plist = p.page_range
    return render(request,"myweb/stu.html",{'stulist':list2,'pIndex':pIndex,'plist':plist})
```

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Web的使用操作</title>
  <!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">

</head>
<body>
    <center>
		<h1>信息分页实例</h1>
		<a href="{% url 'index' %}">返回首页</a>
        <br/><br/>
        <table width="70%" border="1">
            <tr>
                <th>学号</th>
                <th>姓名</th>
                <th>年龄</th>
                <th>性别</th>
                <th>班级</th>
            </tr>
            {% for stu in stulist %}
                <tr>
                   <td>{{ stu.id }}</td> 
                   <td>{{ stu.name }}</td> 
                   <td>{{ stu.age }}</td> 
                   <td>{{ stu.sex }}</td> 
                   <td>{{ stu.classid }}</td> 
                </tr>
            {% endfor %}
        </table>
        <br/>
            <ul class="pagination">
            {%for pindex in plist%}
                <li><a href={% url 'stu' pindex %}>{{pindex}}</a>&nbsp;&nbsp;&nbsp;&nbsp;</li>
            {% endfor %}
            </ul>
    </center>
</body>
</html>
```

## 城市的多级联动

```
    # 城市级联操作
    url(r'^showdistrict$', views.showdistrict, name='showdistrict'),
    url(r'^district/([0-9]+)$', views.district, name='district'),
]
```

```
# 加载城市级联信息操作模板
def showdistrict(request):
    return render(request,"myweb/district.html")

# 加载对应的城市信息，并json格式ajax方式响应
def district(request,upid):
    dlist = District.objects.filter(upid=upid)
    list = []
    for ob in dlist:
        list.append({'id':ob.id,'name':ob.name})
    return JsonResponse({'data':list})
```

```
{% load static from staticfiles %}
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Web的使用操作</title>
	<style>
		select{margin:10px;}
	</style>
	<!-- <script type="text/javascript" src="/static/js/jquery-1.8.3.min.js"></script> -->
	<script type="text/javascript" src="{% static 'js/jquery-1.8.3.min.js' %}"></script>
	<script type="text/javascript">
		//jQuery入口程序
		$(function(){
			$.ajax({
				url: "{% url 'district' 0 %}",
				type: 'get',
				data: {},
				dataType:'json',
				success:function(res){
					var data = res.data;
					for(var i=0;i<data.length;i++){
						$('<option value="'+data[i].id+'">'+data[i].name+'</option>').appendTo('select:last')
						//$('select:last').append('<option value="'+data[i].id+'">'+data[i].name+'</option>'); 
					
					}
				},
				error:function(){
					alert("ajax加载失败！");
				}
			});


			//获取最后一个下拉框并添加选中事件
			$("select").live('change',function(){
				//获取选中的id号
				var id = $(this).val();
				$(this).nextAll().remove();
				$.ajax({
					url: "/district/"+id,
					type: 'get',
					data: {},
					dataType:'json',
					success:function(res){
						if(res.data.length<1)
							return;
						var data = res.data;
						var select = $("<select></select>")
						for(var i=0;i<data.length;i++){
							$('<option value="'+data[i].id+'">'+data[i].name+'</option>').appendTo(select)
							//$('select:last').append('<option value="'+data[i].id+'">'+data[i].name+'</option>'); 
						}
						$("select:last").after(select);
					}
				});
			});

		});
	</script>
</head>
<body>
		<h1>Ajax的城市级联信息操作</h1>

		<br/>

		<select>
			<option>-请选择-</option>
		</select>
		
</body>
</html>
```

## 错误日志

```
看下面前请先确定
	1 确保每个代码页都保存了
	2 重启一下服务实施
	3 看页面下面给的错误的地方,看是不是单词写错了
	4 你可以看下面的错误了

in....      缩进错误
sock    	数据库启动错误		service mysqld restart
404			连接成功,地址栏写的不对

"Table 'myshop.django_session' doesn't exist")
需要执行数据迁移     $ python manage.py migrate

ProgrammingError at /myadmin/orders//
(1146, "Table 'myshop.myadmin_orders' doesn't exist")
表找不见,后台需要在模板处改名				class Meta:
										db_table = "myweb_orders"
```
```
NoReverseMatch at /myadmin/ordersedit/1
Reverse for 'myadmin_ordersedit' with no arguments not found. 1 pattern(s) tried: ['myadmin/ordersedit/(?P<uid>[0-9]+)$']

在html里面少写了一个参数 
<form id="edit-profile" class="form-horizontal" action="{% url 'myadmin_ordersupdate' order.id %}" enctype="multipart/form-data" method="post">
```
### 判断

```
两层判断
<td>
  {% if stu.sex == 1 %}
  男
  {% else %}
  女
  {% endif %}
</td>
三层判断
{% if stu.state == 1 %}
  启用
  {% elif stu.state == 2 %}
  禁用
  {% else %}
  后台管理员
{% endif %}
```
### 一些不会的方法

```
计算总价	数量是shop.m		单价是shop.price
	总价   <h5 id="xiaoji" class="xj">{% widthratio shop.price 1 shop.m %}</h5>
	
	
特殊的提交url方式并进行加减
	减
	<button  class="col-md-2 btn-1 col-xs-2" onclick="window.location='{% url 'gwcchange' %}?sid={{shop.id}}&m={{shop.m|add:-1}}'" >-</button>
	
	加
	<button  class="col-md-2 btn-2 col-xs-2"  onclick="window.location='{% url 'gwcchange' %}?sid={{shop.id}}&m={{shop.m|add:1}}'">+</button>
```

    