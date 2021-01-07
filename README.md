# express-session

对express-session功能增强。可同时设置两个 `Set-cookie` 

## 设置一个

同 [github](https://github.com/expressjs/session)
## 设置两个

两个 Cookie 都用于记录同一个sid，但一个设置为 SameSite: None; Secure，另外一个使用默认值。
然后在处理 Session 时，兼容这两种 Cookie

```javascript
const session = require('session');

app.use(session(
  {
    secret: 'keyboard cat',
    name: 'first',
    cookie: {maxAge: 60000, samesiteWithoutSecure: true}
  }));
```

### 使用哪一个name

获取cookieID 时，如果同时设置了两个 `Set-cookie`, 那么，
- 当请求协议为 **HTTP** 时，则使用第一个配置项中的name，例如上面例子中的`first`
- 当请求协议为 **HTTPS** 时，则在传递的name的基础上拼接'-secure'，例如上面例子,就会变成中的`first-secure`