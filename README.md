# skiff-k8s-site-template

I really liked the idea of [Skiff](https://github.com/basecamp/kamal-skiff/tree/main) but let's make it easily works for k8s instead of [Kamal](https://github.com/basecamp/kamal).

Because we can do some "programming" in deployments in k8s we don't need a custom docker image and also no container registry is required.

Use this repo as a template (the same as the original from kamal-skiff). Clone it, use the "Use this template" button and (vibe) code your static website.

## Development

```bash
docker run -it --rm -p 4000:80 -v ./public:/site/public -v ./config:/etc/nginx/conf.d nginx

open http://localhost:4000
```

## Deployment

Once you build your site, pushed it to a git repo you can use <https://github.com/mvanduijker/k8s-skiff-kustomize> to deploy to your k8s cluster with kustomize.

## Acknowledgements

Thanks [dhh](https://github.com/dhh) and [37 Signals](https://37signals.com/) for making awesome stuff and the open source gifts they bring to us.

