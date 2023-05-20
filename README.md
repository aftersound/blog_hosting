# Create OpenResty docker image which supports https with Let's Encrypt certificate auto-renewed.

nginx natively supports https, however it is quite a manual process to update SSL private key and certificate for 
a nginx server. OpenResty adds dynamic configuration to nginx and some of its addon Lua modules can manage the 
lifecycle of SSL key/certificate without manual intervention. 

Let's Encrypt certificates are free but trusted by most browsers. However, the certificate issued by Let's Encrypt
expires every 90 days. resty-auto-ssl, a Lua module for OpenResty, automatically renews Let's Encrypt key/certificate 
for OpenResty server before SSL key/certificate expires.

This repository includes a dockerfile and also a OpenResty configuration which you can use to create an OpenResty 
docker image which supports https with auto-renewed Let's Encrypt certificate. 

```
# 1. clone this git repository
git clone https://github.com/aftersound/blog_posting

# 2. enter project root directory
cd blog_posting

# 3. build docker image, assuming site domain name is myblog.com
docker build -t openresty --build-arg CN=yourblog.com $(pwd)/openresty/docker

# 4. run docker image
docker run -it -p 80:80 -p 443:443 \
-v $(pwd)/openresty/nginx/conf/nginx.conf:/usr/local/openresty/nginx/conf/nginx.conf \
-v $(pwd)/_site:/usr/share/_site \
openresty
```

Try to visit https://localhost in browser. The browser might complain the site is not secure, which is fine. The reason 
is Let's Encrypt won't be able to issue certificate for localhost or LAN IP. You are good as long as you see the page 
"Welcome to OpenResty with https certificate auto-renewed!". 
