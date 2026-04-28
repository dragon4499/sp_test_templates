# sp_test_templates

```java
// SUB3 - HTTP Server w/ Jetty
public static void main(String[] args) {
  Server server = new Server(8080);

  ServletContextHandler context = new ServletContextHandler(ServletContextHandler.SESSIONS);
  context.setContextPath("/");

  // 기능별 servlet 추가
  context.addServlet(new ServletHolder(new FirstServlet()), "/first");
  context.addServlet(new ServletHolder(new SecondServlet()), "/second");

  server.setHandler(context);
  server.start();
  server.join();
}

static class FirstServlet extends HttpServlet {
  @Override
  protected void doPost(HttpServletRequest request, HttpServletResponse response) {
    // request
    FirstRequest body = new Gson().fromJson(request.getReader(), FirstRequest.class);  // request body 파싱

    // response
    response.getWriter().write(new Gson().toJson(new FirstResponse()));  // response body 작성
    response.setStatus(HttpServletResponse.SC_OK);
    response.setCharacterEncoding("UTF-8");
    response.setContentType("application/json");
  }
}
```
