# fetchOnce
高阶函数，将其包裹一个返回 `promise` 的请求函数，无论该包裹函数调用几次，都确保只真正请求一次。<br>
支持将请求结果存储到 `内存`、`localStorage`、`sessionStorage` 中。<br>
> 错误重试机制：如果一批请求中，有一个成功了，则所有的请求都成功；只有全部失败了，请求才算失败。


## 安装
```bash
npm install @1eeing/fetchonce --save
```


## 如何使用
```js
import fetchOnce from '@1eeing/fetchonce'

const getUserInfo = () => {
  return fetch('test.com');
};

const getUserInfoFetchOnce = fetchOnce(getUserInfo);

getUserInfoFetchOnce().then(res => {
  console.log(res);
})
```

如果需要存储到sessionStorage中
```js
import fetchOnce from '@1eeing/fetchonce'

const getUserInfo = () => {
  return fetch('test.com');
};

const getUserInfoFetchOnce = fetchOnce(getUserInfo, {
  type: 'session',
  key: 'userInfo'
});

getUserInfoFetchOnce().then(res => {
  console.log(res);
})
```


## 参数说明
### fn
请求函数，返回一个promise

### options?
可选配置

#### options.type
存储类型，`local | session | memory` 三个值可选，默认存储到内存中。表示存储到哪

#### options.key
当需要存储到storage中时，需要传入一个自定义key
