# Chapter 1: Introduction to Tekton in OpenShift

Tekton is an open-source framework that allows for the automation of CI/CD pipelines in Kubernetes-based platforms like OpenShift. Tekton provides a set of building blocks, such as Tasks, Pipelines, and Triggers, that allow you to define, run, and manage your continuous integration and delivery pipelines.

## Welcome to the Pipeline (Introduction)

OpenShift Pipelines is a cloud-native, continuous integration and continuous delivery (CI/CD) solution based on Kubernetes resources.
It uses Tekton building blocks to automate deployments across multiple platforms by abstracting away the underlying implementation details. Tekton introduces a number of standard Custom Resource Definitions (CRDs) for defining CI/CD pipelines that are portable across Kubernetes distributions.
OpenShift Pipelines provide a set of standard Custom Resource Definitions (CRDs) that act as the building blocks from which you can assemble a CI/CD pipeline for your application.

### Key Features

- OpenShift Pipelines is a serverless CI/CD system that runs `Pipelines` with all the required dependencies in isolated containers.
- OpenShift Pipelines are designed for decentralized teams that work on microservice-based architecture.
- OpenShift Pipelines use standard CI/CD pipeline definitions that are easy to extend and integrate with the existing Kubernetes tools, enabling you to scale on-demand.
- You can use OpenShift Pipelines to build images with Kubernetes tools such as Source-to-Image (S2I), Buildah, Buildpacks, and Kaniko that are portable across any Kubernetes platform.
- You can use the OpenShift Container Platform Developer Console to create Tekton resources, view logs of Pipeline runs, and manage pipelines in your OpenShift Container Platform namespaces.

## OpenShift Pipelines Concepts

### Task

A `Task` is the smallest configurable unit in a `Pipeline`. It is essentially a function of inputs and outputs that form the Pipeline build. It can run individually or as a part of a Pipeline. A `Pipeline` includes one or more `Tasks`, where each `Task` consists of one or more `Steps`. `Steps` are a series of commands that are sequentially executed by the `Task`.

### TaskRun

A `TaskRun` is automatically created by a `PipelineRun` for each `Task` in a `Pipeline`. It is the result of running an instance of a `Task` in a `Pipeline`. It can also be manually created if a `Task` runs outside of a `Pipeline`.

### Pipeline

A `Pipeline` consists of a series of `Tasks` that are executed to construct complex workflows that automate the build, deployment, and delivery of applications. It is a collection of parameters and one or more `Tasks`.

### PipelineRun

A `PipelineRun` is the running instance of a `Pipeline`. A `PipelineRun` initiates a `Pipeline` and manages the creation of a `TaskRun` for each `Task` being executed in the `Pipeline`.

### Workspace

A `Workspace` is a storage volume that a `Task` requires at runtime to receive input or provide output. A `Task` or `Pipeline` declares the `Workspace`, and a `TaskRun` or `PipelineRun` provides the actual location of the storage volume, which mounts on the declared `Workspace`. This makes the `Task` flexible, reusable, and allows the `Workspaces` to be shared across multiple Tasks.

### Trigger

A `Trigger` captures an external event, such as a Git pull request and processes the event payload to extract key pieces of information. This extracted information is then mapped to a set of predefined parameters, which trigger a series of tasks that may involve creation and deployment of Kubernetes resources. You can use `Triggers` along with `Pipelines` to create full-fledged CI/CD systems where the execution is defined entirely through Kubernetes resources.

## Create an OpenShift Project

Run the following command to create an OpenShift project:

```bash
oc new-project $(oc whoami)
```

## Using Pipelines - the Basics

Now that we understand (or at the very least familiarized) with all the concepts we can start by making sure that OpenShift Pipeline is install on our system.
We can do that by quering for `Pipeline` resource:

```bash
oc get pipelines
```

If the output is the message:

```
error: the server doesn't have a resource type "pipelines"
```

Then OpenShift Pipelines has not been installed. If the output is of the form:

```
No resources found in <project> namespace.
```

Then OpenShift Pipelines has been installed.

In our Scenario we need to Install RedHat Pipelines aka Tekton first.

There are two Scenarios howto do this ... in Chapter 2.
