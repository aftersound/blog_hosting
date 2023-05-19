# Creat OpenResty docker image which supports https with let's encrypt certificate auto-renewed.

Let's encrypt certificates are free and trusted by most browsers. However, the certificate issued by Let's encrypt
expires every 90 days. resty-auto-ssl is a Lua module for OpenResty which automatically renews Let's encrypt
certificate.

```
# 1. cd project root directory

# 2. build docker image, assuming site domain name is myblog.com
docker build -t openresty --build-arg CN=myblog.com $(pwd)/openresty/docker

# 3. try to run docker image
docker run -it -p 80:80 -p 443:443 -v $(pwd)/openresty/nginx/conf/nginx.conf:/usr/local/openresty/nginx/conf/nginx.conf -v $(pwd)/_site:/usr/share/_site openresty
```

Try to visit https://localhost in browser, which might complain the certificate is not secure. The reason is Let's
encrypt won't be able to issue certificate for localhost or LAN IP. As long as you see page "Welcome to OpenResty with
https certificate auto-renewed!", it's fine. 