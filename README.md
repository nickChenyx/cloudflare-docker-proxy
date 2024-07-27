# cloudflare-docker-proxy

![deploy](https://github.com/nickChenyx/cloudflare-docker-proxy/actions/workflows/deploy.yaml/badge.svg)

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/nickChenyx/cloudflare-docker-proxy)

## Deploy

1. click the "Deploy With Workers" button
2. follow the instructions to fork and deploy(*MUST ENABLE GITHUB ACTION*)
3. update routes as you requirement

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/nickChenyx/cloudflare-docker-proxy)

## Routes configuration tutorial

1. use cloudflare worker host: only support proxy one registry
   ```javascript
   const routes = {
     "${workername}.${username}.workers.dev/": "https://registry-1.docker.io",
   };
   ```
2. use custom domain: support proxy multiple registries route by host
   ```javascript
   const routes = {
     "docker-proxy.your-custom-domain.com": "https://registry-1.docker.io",
     "quay-proxy.your-custom-domain.com": "https://quay.io",
     "gcr-proxy.your-custom-domain.com": "https://k8s.gcr.io",
     "k8s-gcr-proxy.your-custom-domain.com": "https://k8s.gcr.io",
     "ghcr-proxy.your-custom-domain.com": "https://ghcr.io",
   };
   ```

## Config Docker mirrors
1. modify `/etc/docker/daemon.json`, add **registry-mirrors** as follow:
   - if you choose **4.1 use cloudflare worker host**.   
     Change the following **url** to your **actually url** (which you can find in **Preview** or **Routes** of your worker).
    ```javascript
    {
        "registry-mirrors": ["https://<workername>.<username>.workers.dev"]
    }
    ```
    - if you choose **4.2 use custom domain**
    ```javascript
    {
        "registry-mirrors": ["https://docker-proxy.your-custom-domain.com"]
    }
    ```
2. restart docker daemon
```
   systemctl restart docker.service
```

**Enjoy yourself!**
  
