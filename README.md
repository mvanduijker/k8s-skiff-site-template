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

Once you built your site and pushed it to your git repo you can deploy with helm or kustomize.
After deployment you can just edit your site and push.
The changes will automatically be applied.

### Helm

Add the helm repo.

```console
helm repo add mvanduijker https://mvanduijker.github.io/mvanduijker-helm-charts
helm repo update
```

Example to deploy with Traefik as ingress controller with automatic let's encrypt certificate.

```console
helm upgrade --install --create-namespace -n hello-world hello-world mvanduijker/k8s-skiff \
  --set 'secret.git_url=https://github.com/mvanduijker/k8s-skiff-site-template' \
  --set 'config.host=hello-world.duyker.nl' \
  --set 'config.secretName=hello-world-k8s-skiff-tls' \
  --set "ingress.enabled=true" \
  --set 'ingress.className=traefik' \
  --set 'ingress.annotations.cert-manager\.io/cluster\-issuer=letsencrypt-prod'
```

For more info check the [chart](https://github.com/mvanduijker/mvanduijker-helm-charts/tree/main/charts/k8s-skiff).

### Kustomize

Clone or fork <https://github.com/mvanduijker/k8s-skiff-kustomize>.
Change the hello-world overlay or create your own to your liking.

To deploy:

```console
kubectl apply -k hello-world # your overlay name
```

## Acknowledgements

Thanks [dhh](https://github.com/dhh) and [37 Signals](https://37signals.com/) for making awesome stuff and the open source gifts they bring to us.
