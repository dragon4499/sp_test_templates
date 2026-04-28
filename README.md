# sp_test_templates

```java
// SUB3,4 - HTTP Server w/ Jetty
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
    FirstRequest bodyAsObject = new Gson().fromJson(request.getReader(), FirstRequest.class);  // request body 파싱 (to Object)
    JsonObject bodyAsJson = JsonParser.parserReader(request.getReader());  // request body 파싱 (to Json)

    // response
    response.getWriter().write(new Gson().toJson(new FirstResponse()));  // response body 작성 (from Object)
    response.getWriter().write(responseJson.toString());  // response body 작성 (from Json)

    response.setStatus(HttpServletResponse.SC_OK);
    response.setCharacterEncoding("UTF-8");
    response.setContentType("application/json");
  }
}
```

```java
// SUB3,4 - HTTP Client w/ Jetty
public static void main(String[] args) {
  HttpClient client = new HttpClient();
  client.start();

  // Request 생성 (POST)
  Request req = client.newRequest("http://127.0.0.1:8080/path").method(HttpMethod.POST);
  req.header(HttpHeader.CONTENT_TYPE, "application/json");
  req.content(new StringContentProvider("request body", "UTF-8");

  // Response 파싱
  ContentResponse res = request.send();
  String response = res.getContentAsString();

  client.stop();
}
```
