###问题描述：
cookie是什么？servlet中cookie是什么？servlet中如何设置cookie？什么时候会设置cookie？为什么第一次访问jsp页面会设置一个cookie?为什么```[HttpServletRquest.getSession();](https://github.com/jboss/jboss-servlet-api_spec/blob/master/src/main/java/javax/servlet/http/HttpServletRequest.java#L539)```会设置一个JSESSIONID的cookie？

###什么是cookie？
cookie 严格来将是http cookie。cookie是http状态管理的原理。[rfc6365规范](https://tools.ietf.org/html/rfc6265)

###servlet中cookie是什么？
在Servlet中```[javax.servlet.http.Cookie](https://github.com/jboss/jboss-servlet-api_spec/blob/master/src/main/java/javax/servlet/http/Cookie.java)```就是http cookie的实现。

###什么时候会设置cookie？

###为什么第一次访问jsp页面会设置一个cookie？
这里所说的第一次是指当客户端浏览器与服务端还没有建立回话或者回话超时。如果jsp没有显示的使用```<%@page Session=”false”%>```关闭session的话，则jsp页面默认都是开启Session的,也就是jsp存在session内置对象的原因。

参考：
-[【转】WEB应用中的SESSION知多少?——iteye](http://hw1287789687.iteye.com/blog/1968385) 
-[Why set a JSP page session = “false” directive?——stackoverflow](http://stackoverflow.com/questions/5515729/why-set-a-jsp-page-session-false-directive)

也可以到tomcat下看下jsp生成的对应的Servlet，关键代码如下
```
 public void _jspService(final javax.servlet.http.HttpServletRequest request, final javax.servlet.http.HttpServletResponse response)
        throws java.io.IOException, javax.servlet.ServletException {

final java.lang.String _jspx_method = request.getMethod();
if (!"GET".equals(_jspx_method) && !"POST".equals(_jspx_method) && !"HEAD".equals(_jspx_method) && !javax.servlet.DispatcherType.ERROR.equals(request.getDispatcherType())) {
response.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, "JSPs only permit GET POST or HEAD");
return;
}

    final javax.servlet.jsp.PageContext pageContext;
    javax.servlet.http.HttpSession session = null;
    final javax.servlet.ServletContext application;
    final javax.servlet.ServletConfig config;
    javax.servlet.jsp.JspWriter out = null;
    final java.lang.Object page = this;
    javax.servlet.jsp.JspWriter _jspx_out = null;
    javax.servlet.jsp.PageContext _jspx_page_context = null;


    try {
      response.setContentType("text/html;charset=UTF-8");
      pageContext = _jspxFactory.getPageContext(this, request, response,
      			null, true, 8192, true);
      _jspx_page_context = pageContext;
      application = pageContext.getServletContext();
      config = pageContext.getServletConfig();
      session = pageContext.getSession();//这个其实调用的就是HttpServletRquest.getSession();
      out = pageContext.getOut();
      _jspx_out = out;

      out.write("\n");
      out.write("\n");
      out.write("<html>\n");
      out.write("<head>\n");
      out.write("    <title>$Title$</title>\n");
      out.write("</head>\n");
      out.write("<body>\n");
      out.write("$END$\n");
      out.write("</body>\n");
      out.write("</html>\n");
    } catch (java.lang.Throwable t) {
      if (!(t instanceof javax.servlet.jsp.SkipPageException)){
        out = _jspx_out;
        if (out != null && out.getBufferSize() != 0)
          try {
            if (response.isCommitted()) {
              out.flush();
            } else {
              out.clearBuffer();
            }
          } catch (java.io.IOException e) {}
        if (_jspx_page_context != null) _jspx_page_context.handlePageException(t);
        else throw new ServletException(t);
      }
    } finally {
      _jspxFactory.releasePageContext(_jspx_page_context);
    }
  }
```

###为什么```[HttpServletRquest.getSession();](https://github.com/jboss/jboss-servlet-api_spec/blob/master/src/main/java/javax/servlet/http/HttpServletRequest.java#L539)```会设置一个JSESSIONID的cookie？

