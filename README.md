# h5-fileuploader
A javascript file uploader based on html5

# Usage

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo</title>
    <script src="index.js"></script>
</head>
<body>
</body>
</html>
```

```javascript
var up = new FileUploader('myfile', {
    // 服务端接收文件的名称
    fieldName: 'file'
    // 是否自动上传
    ,auto: false
    // 是否多选
    ,multiple: true
    // 接收的文件类型
    ,accept: 'image/jpg, image/jpeg, image/png, image/gif'
    // 文件大小限制
    ,fileSizeLimit: 102410245  // 5Mb
});

// 其他一些配置
// 服务器地址
up.configs.server = '/api/upload';
/**
 * 以 form 方式传到服务器的一些额外数据
 */
up.configs.postParams = {
    token: 'xxx',
    otherinfo: 'xxx'
};
/**
 * 设置一些 header 头信息
 */
up.configs.headers = {
    'csrf': 'xxx'
};

/**
 * 选择的文件加入队列后触发
 */
up.fileQueuedHandler = function(file) {
     // 可以在这里渲染上传进度页面
     console.log('one file queued: ', file);
}

/**
 * 多选情况下当所有文件都加入队列后触发
 */
up.filesQueuedCompleteHandler = function(obj) {
     // 非自动上传模式下，可以在这里调用上传方法手动上传
     console.log('all files queued: ', obj);
     
     // up.startUpload();
}

/**
 * 上传进度回调
 */
up.uploadProgressHandler = function(file, percent) {
     // 可以在这里处理进度条
     console.log(percent);
}

/**
 * 当有文件上传成功是触发
 */
up.uploadSuccessHandler = function(file, serverData) {
     // serverData 为服务器返回的数据
     console.log(serverData);
}

/**
 * 当所有文件都上传成功后触发
 */
up.uploadCompleteHandler = function() {
     console.log('upload complete');
}
```

# Support

Theoretically supports all html5 browsers.

+ IE 10+

+ Chrome

+ Firefox

+ Safari