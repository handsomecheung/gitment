# Gitment

[中文说明](README.zh_cn.md)

This project is forked from [imsun/gitment](https://github.com/imsun/gitment).

## Usage

See [imsun/gitment](https://github.com/imsun/gitment) for details.

## Note

There are two things changed over the original project:

1. change proxy server to [https://gh-oauth.print4d.org](https://gh-oauth.print4d.org) from [https://gh-oauth.imsun.net](https://gh-oauth.imsun.net), whose SSL certificate has expired

2. [https://gh-oauth.print4d.org](https://gh-oauth.print4d.org) implements a secret key encryption API, by which you don't need to place cleartext of github client secret key in frontend code. Of course, **use `client_encoded_secret` in the configuare instead of `client_secret`**:

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

Where `client_encoded_secret` can be generated by the follow command:

```
curl -XPOST 'https://gh-oauth.print4d.org/encoded_secret' --data "client_secret=your-client-secret" --data "host=http://yourhost"
```
