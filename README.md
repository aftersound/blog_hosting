# Create OpenResty docker image which supports https with let's encrypt certificate auto-renewed.

Let's Encrypt certificates are free and trusted by most browsers. However, the certificate issued by Let's Encrypt
expires every 90 days. resty-auto-ssl, a Lua module for OpenResty, automatically renews certificate for OpenResty 
server.

```
# 1. clone this git repository
git clone https://github.com/aftersound/blog_posting

# 2. enter project root directory
cd blog_posting

# 3. build docker image, assuming site domain name is myblog.com
docker build -t openresty --build-arg CN=yourblog.com $(pwd)/openresty/docker

# 4. run docker image
docker run -it -p 80:80 -p 443:443 -v $(pwd)/openresty/nginx/conf/nginx.conf:/usr/local/openresty/nginx/conf/nginx.conf -v $(pwd)/_site:/usr/share/_site openresty
```

Try to visit https://localhost in browser. The browser might complain the site is not secure, which is fine. The reason 
is Let's Encrypt won't be able to issue certificate for localhost or LAN IP. As long as you see page "Welcome to 
OpenResty with https certificate auto-renewed!", it's fine. 
