## Flask

### 1. Flask 参数:
```
   def __init__(self, import_name, static_path=None, static_url_path=None,
                   static_folder='static', template_folder='templates',
                   instance_path=None, instance_relative_config=False,
                 root_path=None):
  
  可以指定 import_name, static_folder, template_folder
  
  默认的 static 文件夹： static
  默认的 template 文件夹: templates
  如果要指定 静态文件路径： 设置 static_folder, 指定 模板路径： 设置 template_folder

```

### 2. flask 获取参数


```
   获取post/PUT 数据:
   request.form.get( field_name ) 不要使用 request.form[ field_name ], 当 field_name 不存在时， 
   request.form[ field_name ] 会抛出异常
   
   获取 get 请求数据：
   request.args.get( field_name )
   
   获取 文件上传数据：
   request.files.get( file_field )
   
   request.values 保存 POST, GET 的数据
   
   request.data 保存不能处理的 mimetype 的数据， 以字符串保存
   
   path : 保存请求的 url
   
   如果时数组： 使用 getlist( field_name )
```
