# Gitment

该项目基于 [imsun/gitment](https://github.com/imsun/gitment)。

## 使用方法

参考原始项目 [imsun/gitment](https://github.com/imsun/gitment).

## 说明

基于 imsun/gitment 修改了以下两点：

1. 将代理服务器 [https://gh-oauth.imsun.net](https://gh-oauth.imsun.net) 修改为 [https://gh-oauth.print4d.org](https://gh-oauth.print4d.org)，解决原服务 HTTPS 证书过期的问题

2. [https://gh-oauth.print4d.org](https://gh-oauth.print4d.org) 实现了 Secret Key Encryption API，用于加密 Github Client Secret Key，以避免将 Secret Key 明文暴露在前端代码中。相应地，**配置中原本的 `client_secret` 需要改为 `client_encoded_secret`**：

```javascript
const gitment = new Gitment({
  id: 'Your page ID', // optional
  owner: 'Your GitHub ID',
  repo: 'The repo to store comments',
  oauth: {
    client_id: 'Your client ID',
    client_encoded_secret: 'Your encoded client secret',
  },
})
```

获取 `client_encoded_secret`：

```
curl -XPOST 'https://gh-oauth.print4d.org/encoded_secret' --data "client_secret=your-client-secret" --data "host=http://yourhost"
```

到时会验证请求的 Referer 是否与传递的 `host` 一致。
