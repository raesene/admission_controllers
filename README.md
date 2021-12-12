# Kubernetes Policy Admission Controller Tests

This is a repository to help in testing the various admission controller projects that are designed to enforce policies in Kubernetes clusters. We use ansible and kind to automate cluster provisioning, and then have a set of test manifests to confirm that they're working as expected.

An idea for this project would be to create sets of manifests that may bypass policies which are not correctly implemented.

## Pre-Requisites

- [kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [ansible](https://github.com/ansible/ansible) . On Ubuntu 20.04+ you can install ansible from the default Ubuntu repositories `apt-get install ansible`
- [kubectl](https://www.downloadkubernetes.com/)

## Policy Admission Controller Projects

- [OPA Gatekeeper](https://github.com/open-policy-agent/gatekeeper)
- [Kyverno](https://kyverno.io/)
- [K-Rail](https://github.com/cruise-automation/k-rail)
- [jsPolicy](https://www.jspolicy.com/)
- [Kubewarden](https://www.kubewarden.io/)

## Creating Policy Enabled Clusters

In each directory named for a project, there is an Ansible Playbook, which you can run to create a kind cluster with the policy engine enabled. Just run `ansible-playbook <name>`. This should startup the cluster and set your kubeconfig to point to the context for that cluster.


## Customkind images

The images used for the clusters are customkind, which is basically the `kindest/node` image with ansible installed, so it works ok with the playbook. you can create one building a Dockerfile that looks something like this (with the helm binary in the relevant dir)

```
FROM kindest/node:v1.23.0

RUN apt update && apt install -y python3

COPY ./files/helm /usr/local/bin/
```