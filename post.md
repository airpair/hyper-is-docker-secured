*Disclaimer: Although I am currently working at HyperHQ, what I wrote in this post are personnal opinions, not approved beforehand by the company.*

If you are a developer or system administrator, with an interest in the current DevOps landscape, you probably have heard about [Docker](http://docker.com). But do you know how secured is Docker today? Here is an analysis of the situation, as it is in June 2015.

## Security matters

Regardless you are starting up, or running a corporate-level project, security will always be part of any decision related to your production system(s). The importance of security makes it difficult for new technologies to be adopted, and may slow down their development; but not if security has been placed at the top priority since the origin of the idea.

[Docker cares about security](https://www.docker.com/resources/security/). We can read on their website, "We take the security of Docker very seriously. We know Docker is important to you and so we respond to security issues and concerns promptly. When necessary we will release new versions to address vulnerabilities or security issues".

A couple of months ago, Docker Inc. have worked with the Center for Internet Security (CIS) to produce a [benchmark document](https://benchmarks.cisecurity.org/tools2/docker/CIS_Docker_1.6_Benchmark_v1.0.0.pdf) on the security of containers, using Docker.
This document contains a lot of recommendation and good practices, sometimes generic and sometimes very specific, when architecting a production system using Docker containers, such as "Do not mount sensitive host system directories on containers", or "Verify that docker.service file permissions are set to 644 or more restrictive".

![Docker Images Vulnerabilities](https://s3-us-west-1.amazonaws.com/bloghyper/post1/vulnerabilities.png)

*Percentage of official images with vulnerabilities, credit: BanyanOps*

## But, Docker images are said unsafe!?

Recently, an article from BanyanOps stated that [Over 30% of Official Images in Docker Hub Contain High Priority Security Vulnerabilities](http://www.banyanops.com/blog/analyzing-docker-hub/). This scary number has been [argued](http://jpetazzo.github.io/2015/05/27/docker-images-vulnerabilities/) by Jérôme Petazzoni, former developer and thinker at Docker, who said that, although this number may be correct, many of the vulnerable images are voluntary using older and unpatched versions of software, for testing/compatibility purposes.

![Docker bench for Security](https://s3-us-west-1.amazonaws.com/bloghyper/post1/bench_security.gif)

*Docker Bench for Security, credit: Docker Inc.*

### Images need maintainers

Jérôme, in his [post](http://jpetazzo.github.io/2015/05/27/docker-images-vulnerabilities/), also called for **auditing Docker images**, in order to improve their overall security. He recommended the usage of Docker's [Bench for Security](https://github.com/docker/docker-bench-security), which "is a script that checks for all the automatable tests included in the CIS Docker 1.6 Benchmark", being then a complement to the [benchmark document](https://benchmarks.cisecurity.org/tools2/docker/CIS_Docker_1.6_Benchmark_v1.0.0.pdf) we related before.

In a [recent interview](https://medium.com/s-c-a-l-e/how-containers-became-a-tech-darling-and-why-docker-became-their-poster-child-bfaf9ac87825), Jason Hoffman, head of technology for cloud systems at Ericsson and ex-CTO of cloud computing provider Joyent, said that "Docker’s taking off because it’s the **new package management**". To that end, Docker images lack of any official, maintained, and safe delivery channel (think `apt-get`, `yum`, ...).

Both showed that Docker images need *official* maintainers.

## The need for isolation

We saw that when you run Docker containers, you may be running **uncertainly safe** Images. But, also, your containers may be [uncertainly isolated](https://zeltser.com/security-risks-and-benefits-of-docker-application/).

Although Docker Inc. is putting a lot of efforts toward security, it may sound scary, giving sense to the need for better isolation in case of multi-tenant applications.

![Hybrid Infrastructure by Docker](https://s3-us-west-1.amazonaws.com/bloghyper/post1/docker.png)

*Hybrid infrastructure presented by Docker, credit: Docker Inc.*

In a [white paper](https://d3oypxn00j2a10.cloudfront.net/assets/img/Docker%20Security/WP_Intro_to_container_security_03.20.2015.pdf) published in March 2015, Docker Inc. discussed the possibility of **hybrid solutions (VMs + Containers)** in order to improve isolation, and general security: "Regular VMs function in a way that does not allow them to be efficiently scaled down to the level of running a single application service. A VM can support a relatively rich set of applications but running multiple microservices in a single VM without containers creates conflict issues while running one microservice per VM may not be financially feasible for some organizations. Deploying Docker containers in conjunction with VMs allows an entire group of services to be isolated from each other and then grouped inside of a virtual machine. This approach increases security by introducing two layers, containers and VMs, to the distributed application. Additionally this method employs a more efficient use of resources and can increase the density of containers while decrease the number of VMs required for the defined isolation and security goals".

Convinced that hybrid systems are the right way to maintain a **safe level of security** while using the power and **flexibility** containers provide, a team of professional Linux kernel engineers built **[Hyper](http://hyper.sh)**, [taking the best from both worlds](https://hyper.sh/why-hyper.html).

You can follow [Hyper](http://hyper.sh) on Twitter ([@hyper_sh](https://twitter.com/hyper_sh)) or [Github](https://github.com/hyperhq).

[![Hybrid Infrastructure by Hyper](https://s3-us-west-1.amazonaws.com/bloghyper/post1/hyper.png)](http://hyper.sh)

*Hybrid infrastructure presented by Hyper, credit: HyperHQ Inc.*
