# tekton-dockerimg-build-demo
Simple Tekton pipeline files for a demo of building a Docker container.

This repo contains a Tekton task that will clone a git repository and build/publish a Docker image using Kaniko to a Docker registry. Building a docker image on a Kubernetes host is not advised, so Kaniko is used.

## Pre-req

1) GitHub repository. This example is setup to use a private repository (secrets are used for auth).
2) Docker registry. This example is setup to push an image to a registry (DockerHub in my case).

## Setup

1) Create the namespace 'tekton-demo' or rename the namespace defined in the task-build-img.yml to one that fits your environment.

2) Create the secret used for use with git clone. If using GitHub, you'll need to utilize a Personal Access Token (PAT). This is found in Settings -> Developer tools -> Personal Access Tokens. This secret should co-exist in the namespace you're using for the demo.

```
kubectl create secret generic <SECRET_NAME> --from-literal=username=<USERNAME> --from-literal=password=<PAT> -n <K8S NAMESPACE>
```
3) Kaniko push utilizes a docker-registry secret. This secret should be created in the namespace used for the demo.

```
kubectl create secret docker-registry <SECRET_NAME> --docker-username=<USERNAME> --docker-password=<PASSWORD> --docker-email=<EMAIL> -n <K8S NAMESPACE>
```
