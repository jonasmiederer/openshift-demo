---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: ./logo.png
# some information about your slides, markdown enabled
title: Red Hat OpenShift
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
hideInToc: true
---

# Red Hat OpenShift

Introduction & Demo of OpenShift


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: two-cols
layoutClass: gap-16
---

# Table of contents


<Toc minDepth="1" maxDepth="3"></Toc>

---
transition: fade-out
---

# Intro

This provides a summary of the topic

---
transition: slide-up
level: 2
layout: image-right
image: https://upload.wikimedia.org/wikipedia/commons/d/d8/Red_Hat_logo.svg 
backgroundSize: contain
---

## What is RedHat

- Leading provider of different open-source solutions for enterprises
- Red Hat's portfolio also includes middleware, storage, virtualization, and cloud technologies, catering to various enterprise needs.
- It follows an open-source business model, providing access to its source code and collaborating with the community to develop and enhance its products.
- In 2019, Red Hat was acquired by IBM, but it continues to operate as a separate entity within the IBM Cloud and Cognitive Software division.


---
transition: slide-up
level: 2
layout: two-cols
---

## Notable RedHat Products

<img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Red_Hat_Enterprise_Linux_logo.svg" v-bind="props"/>

- Commercial open-source Linux distribution

- stable and secure operating system platform with long-term support, suitable for mission-critical applications and infrastructure.

- Fedora Linux and CentOS Stream as upstream sources

::right::

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQQhoYUzCXxIkqgwFDAyA8PukHK_T5JgNPc08QdAsvP&s" v-bind="props"/>

- open-source automation tool

- simplifies complex tasks by allowing users to automate repetitive tasks such as software provisioning or application deployment across multiple servers or devices.

- uses a simple and human-readable syntax (YAML) and operates agentlessly, communicating with remote nodes via SSH


---
level: 2
---

## What is Red Hat OpenShift?

- Hybrid cloud application platform
- Built around Linux containers
- Orchestrated and managed by Kubernetes (RHOS builds upon Kubernetes but adds enterprise features and support, including additional tools and services)
- foundation of Red Hat Enterprise Linux (RHEL)


---
level: 2
---

## Red Hat OpenShift vs. Kubernetes

|                                        | Kubernetes | OpenShift |
|----------------------------------------|------------|-----------|
| Multi-container, multi-host scheduling | ✅          | ✅         |
| Self-service provisioning              | ✅          | ✅         |
| Service discovery                      | ✅          | ✅         |
| Persistent Storage                     | ✅          | ✅         |
| Multi-tenancy                          |            | ✅         |
| Networking (SDN)                       |            | ✅         |
| Image Registry                         |            | ✅         |
| Image Build Tools                      |            | ✅         |
| Metrics                                |            | ✅         |
| Log Aggregation                        |            | ✅         |
| Ingress                                |            | ✅         |
| UX: Console, Service Catalog, "oc"     |            | ✅         |
| Secured by Default                     |            | ✅         |

---
level: 1
layout: section
---


# OpenShift Architecture & Concepts


---
level: 2
---

# OpenShift Architecture

- Layered system designed to expose underlying Docker-formatted container image and Kubernetes concepts as accurately as possible
- Focus on easy composition of applications by a developer

Layers:

  - Docker service provides abstraction for packaging and creating container images
  - Kubernetes provides the cluster management and multi-host container orchestration
  - OpenShift Container Platform adds:
    - Source code management, builds, and deployments for developers
    - Managing and promoting images at scale
    - Application management at scale
    - Team and user tracking 
    - Networking infrastructure

---
level: 2
layout: image
image: images/architecture.png
backgroundSize: 80%
---

## OpenShift Architecture


---
level: 2
---

## OpenShift Deployments

OpenShift can be deployed in the cloud, on-premise or hybrid. 

- Red Hat OpenShift on AWS (ROSA)
- Azure Red Hat OpenShift (ARO)
- Red Hat OpenShift Container Platform on GCP
- Red Hat OpenShift on IBM Cloud 
- Red Hat OpenShift Container Platform (self-managed instance in the cloud or on-premise)


---
level: 2
---

# How OpenShift works

- Microservices-based architecture of smaller, decoupled units that work together
  - `etcd` – a clustered key-value store holding data about the objects 
  - REST APIs, exposing each of the core objects
  - Controllers reading those APIs and applying changes to other objects, and report status or write back to to the object


- Controller pattern means that much of the functionality is extensible
- Controllers leverage a reliable stream of changes to the system to sync their view of the system with what users are doing

---
level: 2
---

## OpenShift Resources - Project

Comparable to Kubernetes Namespace, but with additional administrative controls:

- Isolation: Provide a level of isolation and resource management within an OpenShift cluster (sandboxed environment)
- Fine grained control over permissions: Own set of access controls and security policies
- Quotas and limits: Administrators can set limits on the amount of CPU, memory, storage and other resources that each project can consume
- Multi-Tenancy support: organizations can host multiple teams or applications within the same cluster while maintaining isolation and security between them


---
level: 2
---
## OpenShift Container Registry (OCR) / Quay

- Integrated registry that provides a secure and centralized location for storing and managing container images

- facilitates image promotion and lifecycle management by enabling users to tag, version, and promote container images across different environments 

- seamlessly integrates with OpenShift Pipelines, allowing users to automate the build, test, and deployment processes for containerized applications. It provides native support for source-to-image (S2I) builds, Dockerfile builds, and image streams, enabling continuous integration and delivery (CI/CD) workflows.

- Quay is a standalone enterprise-grade CR

---
level: 2
---
## OpenShift Web Console

- Feature-rich GUI to control the OpenShift instance itself as well as workloads and resources running on OpenShift

- Runs itself as a pod on the master node

<img src = "images/web_console.png" />

---
level: 2
---
## OpenShift CLI

`oc`: CLI tool to manage OpenShift Container Platform projects and other resources from a terminal

Examples: 

- `oc cluster-info`
- `oc get projects`
- `oc login <OpenShift API URL> -u <username> -p <password>`
- `oc new-project <project-name>`
- `oc new-app <image-name>`

---
level: 2
---
## OpenShift Core Concepts

Based on Kubernets, extended by OpenShift to provide a more feature-rich development lifecycle platform

- Containers & images &nbsp;&nbsp;➡️ &nbsp;&nbsp;  building blocks for deploying applications
- Pods & services &nbsp;&nbsp; ➡️  &nbsp;&nbsp; inter-container communication
- Projects & users &nbsp;&nbsp; ➡️ &nbsp;&nbsp; organization & separation of users & workloads
- Builds & image streams &nbsp;&nbsp; ➡️ &nbsp;&nbsp;  image building with event stream
- Deployments &nbsp;&nbsp; ➡️ &nbsp;&nbsp; expanded support for software development and deployment lifecycle
- Routes &nbsp;&nbsp; ➡️ &nbsp;&nbsp; service accessibility
- Templates &nbsp;&nbsp; ➡️ &nbsp;&nbsp; multi-object creation based on customized parameters

---
level: 3
---
## OpenShift Core Concepts - Builds

A build is the process of transforming input parameters or source code into a result object (runnable image). A BuildConfig object is the definition of the entire build process.

OpenShift offers 3 different build strategies:

- **Docker build**: Expects a repository with a Dockerfile and all required artifacts to produce a Docker image
- **S2I build**: Source-to-Image build is a tool for building Docker-formatted container images by injecting application source into a container image and assembling a new image
- **Custom build**: allows developers to define a specific builder image responsible for the whole process. The resulting objects are whatever the builder image author has specified

---
level: 3
---
## OpenShift Core Concepts - Deployments

- **Deployment**
  - Native Kubernetes object
  - A deployment is an object type used to manage the rollout and scaling of application replicas (pods) in the cluster
  - Defines the desired state for the application, automatically creating or updating pods as needed to match the desired configuration
  - Supports various strategies, such as rolling updates, blue-green deployments, and canary deployments

- **DeploymentConfig**
  - OpenShift specific resource
  - Provides additional features and capabilities tailored for managing applications within OS
  - e.g. can trigger new deployments with `ConfigChange` or `ImageChange` 


---
level: 1
layout: section
---
# Demo

Deploy application in OpenSHift

---

# Sources

- https://www.openvirtualization.pro/red-hat-openshift-container-platform/

---
layout: center
class: text-center
---

# Learn More

[Documentations](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)
