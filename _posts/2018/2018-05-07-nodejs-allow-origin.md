---
layout: post
title: Node.js设置允许多个域名跨域、或nginx
tags: [nodejs,nginx]
categories: [it]

---

### 1 全局设置: `app.js` 中

```
var orginList = [
  'http://127.0.0.1:4000', 'https://xindot.com', 'https://www.xindot.com'
]
app.all("*", function (req, res, next) {
  if (orginList.includes(req.headers.origin)) {
    //设置允许跨域的域名，*代表允许任意域名跨域
    res.header("Access-Control-Allow-Origin", req.headers.origin);
  }
  //允许的header类型
  res.header("Access-Control-Allow-Headers", "content-type");
  //跨域允许的请求方式
  res.header("Access-Control-Allow-Methods", "DELETE,PUT,POST,GET,OPTIONS");
  next();
})

// 注意：放在路由设置之前
// app.use('/user', require('./routes/user'));
```

### 2 局部路由设置: 比如说在 `routes/user.js` 下面

```
var orginList = [
  'http://127.0.0.1:4000', 'https://xindot.com', 'https://www.xindot.com'
]
router.all("/*", function (req, res, next) {
  if (orginList.includes(req.headers.origin)) {
    //设置允许跨域的域名，*代表允许任意域名跨域
    res.header("Access-Control-Allow-Origin", req.headers.origin);
  }
  //允许的header类型
  res.header("Access-Control-Allow-Headers", "content-type");
  //跨域允许的请求方式
  res.header("Access-Control-Allow-Methods", "DELETE,PUT,POST,GET,OPTIONS");
  next();
})

// 注意：放在路由设置之前
//router.get('/list', (req, res) => { res.send({code:200})} )
```

### 3 如果不想在node项目中设置，可以选择设置nginx

##### 3.1 正则匹配：*[Nginx如何配置跨域(多个域名)](https://blog.csdn.net/moxiaomomo/article/details/82970004){:target="_blank"}*

```
location / {
  set $match "";
  # 支持http及https
  if ($http_origin ~* 'https?://(localhost|.*\.example\.com)') {
    set $match "true";
  }

  if ($match = "true") {
    add_header Access-Control-Allow-Origin "$http_origin";
    add_header Access-Control-Allow-Headers 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
    add_header Access-Control-Allow-Methods GET,POST,OPTIONS,DELETE;
    add_header Access-Control-Allow-Credentials true;
  }
  # 处理OPTIONS请求
  if ($request_method = 'OPTIONS') {
    return 204;
  }
}
```

##### 3.2 map匹配：*[Nginx 允许多个域名跨域访问](https://www.123admin.com/how-to-enable-cross-origin-requests-cors-on-nginx/){:target="_blank"}*

```
map $http_origin $corsHost {
    default 0;
    "~http://www.123admin.com" http://www.123admin.com;
    "~http://m.123admin.com" http://m.123admin.com;
    "~http://wap.123admin.com" http://wap.123admin.com;
}
server {
  listen 80;
  server_name search.123admin.com;
  root /nginx;
  location / {
    add_header Access-Control-Allow-Origin $corsHost;
  }
}
```