# axios

## axios 简介

axios 是一个基于 Promise 用于浏览器和 nodejs 的 HTTP 客户端，它本身具有以下特征：

1. 从浏览器中创建 XMLHttpRequest
2. 从 node.js 发出 http 请求
3. 支持 Promise API
4. 拦截请求和响应
5. 转换请求和响应数据
6. 取消请求
7. 自动转换 JSON 数据
8. 客户端支持防止 CSRF/XSRF

```js
axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});
```