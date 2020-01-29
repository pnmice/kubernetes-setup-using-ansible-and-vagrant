# kubernetes-setup-using-ansible-and-vagrant
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

"Kubernetes Setup Using Ansible and Vagrant" working source files. :heavy_check_mark: :100:

## What is this?
I was trying to learn how to setup a Kubernetes cluster on my machine without `minikube` and I came across this [tutorial](https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant). Unfortunately, by just copying/pasting the configuration files I got a lot of errors and I had to review every single file to make it work. In this repository you can find the resulting working files.

## Prerequisites
- Read the [original tutorial](https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant) (optional);
- Install `VirtualBox`;
- Install `Vagrant`;
- Install `Ansible`.

## How to run
```bash
vagrant up
```

## Access the master
```bash
vagrant ssh master
```

### Check if nodes did join the master successfully
```bash
# Run this from the master
kubectl get nodes
```

## Access nodes
```bash
vagrant ssh node-1
# Or
vagrant ssh node-2
```

## By the way...
I don't understand everything in these files. If you have a
good understanding of the tools (Vagrant, Ansible and Kubernetes),
your pull requests are welcome to make this repository easier
to understand for beginners.
