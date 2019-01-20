# RainbowChat工具集成到towerxi App 文档

- 这个接口是用来实现塔兮原来的系统一键登录聊天系统的接口，具体RainbowChat 的接口要看 【RainbowChat4.0-HttpRest接口手册-v1.9.pdf】

## 接口说明

### 接口URL

    http://localhost:8080/towerchat/rest_post

> 其中[http://localhost:8080/towerchat] 是塔兮IM 的入口URL 目前测试环境用的是 [http://towerxi.com/towerchat/]

### 请求方法

    POST

### 请求内容(JSON)

```JSON
{
"processorId":1018,
"newData": "{
\"tid\": \"2c93b3ca63fd01ea01641160ee8b0042\", 
\"uid\": \"\", 
\"nickName\": \"3333333\",
\"userSex\": \"1\",
\"osType\": 0
}"
}
```

### okhttp 代码模板

```JAVA
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("text/plain");
RequestBody body = RequestBody.create(mediaType, "{\r\n\"processorId\":1018,\r\n\"newData\": \"{\r\n\\\"tid\\\": \\\"2c93b3ca63fd01ea01641160ee8b0042\\\", \r\n\\\"uid\\\": \\\"\\\", \r\n\\\"nickName\\\": \\\"3333333\\\",\r\n\\\"userSex\\\": \\\"1\\\",\r\n\\\"osType\\\": 0\r\n}\"\r\n}");
Request request = new Request.Builder()
  .url("http://localhost:8080/towerchat/rest_post")
  .post(body)
  .addHeader("Content-Type", "application/json")
  .addHeader("cache-control", "no-cache")
  .addHeader("Postman-Token", "c86e4700-d3b0-44b6-b9c4-6d14edc62826")
  .build();

Response response = client.newCall(request).execute();
```

### 请求内容说明

|参数|数据类型|说明|
|---:|:---|:---|
|processorId|Int| 108 新增 塔兮快捷登录处理器ID|
|newData|String|内容 请求的内容（进过转义的JSON字符串）|
|-"tid"|String|塔兮用户ID|
|-"uid"|String|塔兮IM 用户ID|
|-"nickName"|String|塔兮用户昵称|
|-"userSex"|String|塔兮用户性别 “1” 男 “0” 女|
|-"osType"|Int|设备类型 0 安卓 1 IOS 2 web|

### 返回类型

    同【RainbowChat4.0-HttpRest接口手册-v1.9.pdf】中  [3.2 【接口 1010】客户端版本更新检查接口] 的返回