## SpringMVC

### 1. Srping MVC 返回json

- 使用 @ResponseBody 和 Jackson 返回json
```
  1. 要配置jackson 2, 并且要使用 jackson-core jackson-databind,jackson-annotation 三个jar, 在pom文件中引入 jackson-core, 
    只会引入单个jackson-core 文件， 可以引入 jackson-databind, 这样可以同时引入以上三个 jar 包。
    
  2. 使用 @ResponseBody 注解 返回值, 或者使用 @RestController 注解替代 @Controller
```

- 使用 Json 框架把数据转换成json 字符串， 在使用 HttpRequestResponse 的 out.write( jsonstr ) 输出 json 字符串
```
  注意要设置 Content-Type : application/json
  public static void writeJsonResponse( HttpServletResponse response, String res , int statusCode) {
			try {
				response.setContentType("application/json;charset=UTF-8");
				response.setCharacterEncoding("UTF-8");
				response.setHeader("Charset", "UTF-8");
				response.setHeader("Cache-Control", "no-cache");
				response.setStatus(statusCode);
				response.getWriter().print(res);
			} catch (IOException e) {
			}
		}
```
