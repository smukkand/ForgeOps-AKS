# Kustomize

Sample [Kustomize](https://kubectl.docs.kubernetes.io/pages/app_customization/introduction.html) deployments.

[ship](https://www.replicated.com/ship/) was used to generate the kustomize from our exiting helm charts.

The organization is experimental - feedback welcome.

If you are not familiar with Kustomize please refer to the link above - the explanation below will make a lot more sense.

TL;DR; - Kustomize is based on patching (json patch and strategic merge patch) and overlays.
You create base assets (K8S yaml files), and patch those. Those in turn can be used as a new base, and so on. You can nest these to any 
arbitrary depth.

## Organization

The top level directory includes the products (am, idm, ig, ds) and an "environments"  folder in `env/`.  Environments
pull together ther products into a kustomize deployment. See env/dev for an example.

## Viewing the Kustomize output

You can use `kubectl`  (version 1.14 or higher) or `kustomize`


```bash
cd kustomize/env
# This will show you what is sent to the cluster
kubectl kustomize example
```

## Images

The images referenced in the kustomize files are generic (example: `am`, `ig`), and not
specific to a registry ( `gcr.io/forgerock-io/am:7.0.1` ).

We can not directly deploy these generic images, because we need a docker image
that has the configuration "baked in". This is where skaffold comes in to the picture.
Skaffold will build new docker images that include configuration, and will 
"fix up" the docker image tags in kustomize, replacing the generic names (`am`) with
a specific image name, tagged with a sha hash (dev mode) or a git hash (prod).

See the skaffold [../README.md](../README.md).

## Further Discussion

 * This demonstrates a directory based organization. You can also use git branching. See [this discussion](https://kubectl.docs.kubernetes.io/pages/app_composition_and_deployment/diffing_local_and_remote_resources.html)
