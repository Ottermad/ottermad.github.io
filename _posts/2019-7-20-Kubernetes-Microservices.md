---
layout: post
title: Introduction to Microservices - A reasonable example
author: Charles Thomas
---

This is a work in progress
## Introduction to Microservices - A reasonable example

I built [VLE](https://github.com/Ottermad/VLE) and the original version of [VLEFrontend](https://github.com/Ottermad/VLEFrontend) as a coursework project and have now converted them to use microservices. The purpose of this blog post is to walk you through setting up this project locally and running it on Kubernetes. Hopefully, this will give you a bit of an insight in how to develop microservices and how to use Kubernetes and Docker.

### What are microservices
Traditionally, software is developed is with what is called the Monolith architecture. What this means is that a single large piece of software is developed with all the features needed. But recently a new approach has become popular - microservices. In a microservice architecture, several smaller programs are created - each with a specific task - then they talk to each other to achieve some overarching task.

### What is Kubernetes (k8s)
Kubernetes is a container orchestration system. In order to understand this, we must first define what we mean by container - a container is simply a bundle of software containing some code and all its dependicies so that the code can be run easily on many different systems (for more info see [here](https://www.docker.com/resources/what-container)). There are several pieces of software used to create containers but the one I have used in this project is called Docker. In Docker, you define a blueprint for a container called an image, then each instance of the image is called a container.

In a microservice architecture, each of our services can be bundled in a container (in fact we might have multiple copies of the same container for each service). Now managing these all these containers and enabling these services to talk to each other is the job of Kubernetes. 

### Setup
In order to begin this project you'll need to install Kubectl and Minikube. Kubectl is a command line program for managing Kubernetes clusters and Minikube is a program that sets up a virtual machine with a single node kubernetes cluster on your local machine. 

To install these follow these links: [Install Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) and [Install Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/).

If you also want to make changes and deploy them to your cluster you'll also need to install [Python 3](https://www.python.org/downloads/) and [Docker](https://hub.docker.com/search/?type=edition&offering=community)

To get started following along with project clone this [repo](https://github.com/Ottermad/vle-stack)

### Overview of the Project
The project is a virtual learning enivronment (VLE) that allows a school to add teachers and students then allows teachers to set students homework. 

The frontend of the project has been written in React and can be found under VLEFrontend.

The backend of the project consists of a number of services. The service REST API (found under vle-restapi) acts as an interface between the frontend and the rest of the services this way the frontend only sees a single API no matter how many services are behind it. The vle-user service handles storing users and their schools and the lesson and homework services deal with storing the lessons student attend and the homework they submit for them. There is also a services service which is a helper service that makes it easier to communicate between services. 

You'll notice a couple of other folders that don't correspond to services. vle-internals is a python package that is used by the other services and contains lots of helpful functions such as a decorator to handle permissions. services_extension is another python package that allows services to easily to interact with the Services service.

The final folder is vle-k8s-scripts which stores the yaml files which will be used to configure Kubernetes.


