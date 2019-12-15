
## 本地
```
jekyll server
```

## 打包
```
jekyll build
```

## 黏贴图片上传七牛配置：
- 1.安装插件Markdown
- 2.在settings.json中新增
```
"qiniu.access_key": "******",
"qiniu.secret_key": "******",
"qiniu.bucket": "d-6h5",
"qiniu.domain": "http://img.6h5.cn",
"qiniu.isSaveLocal": false,
"qiniu.localPath": "./img",
"qiniu.remotePath": "xindot-blog/paste/${fileName}"
```