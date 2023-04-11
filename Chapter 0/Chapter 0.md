# Chapter 0: Preparation / Pre Tasks:

In Chapter 0 we will setup our environment in a way that it is usable for our Workshop and have all the required resources for getting our OpenShift 4.X later working with Tekton/ArgoCD

## 1.) DO280 Environment

As our Base Environment we are using the OpenShift Environment in our DO280 Course.

First we need to setup our Workshop Environment which is based upon the Course Environment DO280 v4.12.

For our Tekton/ArgoCD Workshop we need to have an running Lab Environment in which we later will deploy out Red Hat Pipelines and RedHat Git OPS Operators and creating for examples Pipelines.

The Steps to setup the DO280 Environment are descibed in the DO280 Coursematerial that all delegates should download from: [https://rol.redhat.com](https://rol.redhat.com)

The Steps to setup the Environment and check the environment will be explained by the Instructor based upon this Course Material.

There is a Video that is demonstrating how to setup the environment as well:

https://jwp.io/s/KAVC7wF9

## 2.) GitHub

When done with setup the DO280 Course Environment, as Tekton/ArgoCD is based upon the GitOPS Philosophy, we need to get Access to the Exercices / Labs in our Workshop and therefore we need to have a GitHub Repository, or better several Git Repositories for different kind of scenarios.

All Delegates need to have an GitHub Account. Later in this Workshop we will use our Github plus the Git Repository for this Workshop to create individual pipelines in the labs/labs in several Repositories.

To get access to the repositories, "2FA should not been activated or if it is, in Github an Access Token need to be configured to be able to get access to the Git Repositories."

It is possible to have all these Respositories "public", but to have a more "enterprise" feeling it is better to set them on private, as in some Labs we demonstrate how to create secrets to get Access to the Git Repositories.

## 3.) quay.io

All Delegates need to have as well an quay.io account on [https://quay.io](https://quay.io). Your instructor willl guide you through this process.
