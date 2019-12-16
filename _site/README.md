
## 本地
```
jekyll server
```

## 打包
```
jekyll build
```

## 粘贴图片上传七牛配置：
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

## 加入vscode开启了beautify，可以设置忽略选项，避免被格式化
"beautify.ignore": ["**/_includes/**", "**/_layouts/**"]
如果遇到css中遇到jekyll中定义的```{{}}```变量语法警告，css验证也可以关掉
"css.validate": false