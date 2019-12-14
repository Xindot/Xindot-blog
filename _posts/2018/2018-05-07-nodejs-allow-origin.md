---
layout: post
title: Node.js设置允许多个域名跨域
tags: [nodejs]

---


#### 1.全局设置: `app.js` 中

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

#### 2.局部路由设置: 比如说在 `routes/user.js` 下面

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