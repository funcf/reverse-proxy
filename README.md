# reverse-proxy

A simple example app that runs on Cloud Foundry serving as a reverse proxy 
adding Basic Auth to an app with an internal route that can be configured 
with an environment variable and an according network policy.
In addition this example shows how to set CORS and HSTS headers 
in the NGINX config, where also multiple backends and ports can be set.

**Usage:** 
 
```
cf create-app reverse-proxy
cf set-env reverse-proxy BACKEND_URL "https://mydemo.apps.internal:61443"
cf add-network-policy reverse-proxy mydemo --protocol tcp --port 61443
cf push reverse-proxy -b nginx_buildpack
```

Once the app is running, simply call the URL and see the backend app after logging in.

**User:** `Hello`
**Password:** `World!`

[More Details about the NGINX Buildpack](https://docs.cloudfoundry.org/buildpacks/nginx/)

[More Details about Container to Container Networking within Cloud Foudry](https://docs.cloudfoundry.org/concepts/understand-cf-networking.html)

**Good to know (from the link above): To utilize TLS capabilities, the client application can connect to port 61443 on the destination application over HTTPS. Traffic to application container port 61443 is proxied to application port 8080 inside of the container. So the app does not need to implement that. =)**

**Please Note: This is an example app with a unsecure password that you would not have in git without gitcrypt for productive use cases.**
