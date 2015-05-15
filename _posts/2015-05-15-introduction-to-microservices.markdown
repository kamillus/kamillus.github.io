---
layout: post
title:  "Introduction to Microservices"
date:   2015-05-15 09:44:30
categories: microservices, architecture, rest
---
The popularity of web development frameworks, agile processes, and product oriented development is driving application design in a new direction. Microservices provide a new spin on existing principles tackling complexity with tried and true techniques that reduce coupling and increase cohesion. 

Writing with a microservice architecture in mind involves writing small, discrete applications that have a single objective but potentially collaborate to form something greater. Microservices tend to be decentralized; as an example, the data store should not be shared except through an interface potentially resulting in duplicated data. Microservices tend to be small; there should not be any major effort in rewriting a microservice if needed. Lastly, Microservices are evolutionary; the release cycle is more agile with the reduction of complexity.

Due to the inherent decoupling of microservices, effort can be maximized in the development of a product using agile approaches; the teams focus on solving the problem rather than fighting a monolithic technology stack. The technical benefits are numerous including easily pluggable infrastructure, parallelization, and simplified security. Additionally, unit and integration testing becomes simpler while a failure in a microservice does not result in a system failure. Often, in a web application setting, microservices use idempotent RESTful interfaces to communicate between the interface and the service using the HTTP protocol. It is important to note that lightweight and open protocols such as HTTP and data structures utilizing the simplicity of JSON/XML are at the heart of good microservice design. Always bet on simple text representation of data instead of binary blobs to help with 'future-proofing'.

One of the costs of using microservices is the high utilization of network infrastructure, however, it is important not to get caught up in premature optimization. Additionally, it is problematic to segregate existing applications into microservices. Where do application boundaries start and end?

Microservices are currently being utilized by big names such as Amazon and Netflix. Microservices offer a lot at a small sacrifice. Reduced coupling and increased cohesion are a no brainer software quality; The technology is there; Start thinking microservices now!