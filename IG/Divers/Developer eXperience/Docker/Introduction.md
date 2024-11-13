---
title: DOCKER_INTRO_EN
author: Eugénio BAYE
date: 2024-10-19
update: 2024-10-19
version: "1.0"
copyright: © 2024 Eugénio BAYE. Tous droits réservés.
tags:
  - WEB
  - Container
  - Docker
---
# Introduction to Docker

Have you ever heard the phrase "It works on my machine" or struggled with compatibility issues across different environments like Windows and Mac OS? Docker was created in 2013 to solve such problems, and today, it's one of the most critical tools in modern software development, used by 57% of professional developers.

Docker allows us to package our applications and their dependencies into a **container** that ensures consistency across environments. Whether you’re developing, testing, or deploying applications, Docker creates a standardized environment where your app runs the same way everywhere. This makes Docker a must-have skill, especially for developers aiming for high-paying jobs.

## Why Use Docker?

Companies like eBay, Spotify, Uber, and Yelp use Docker because it improves both development and deployment processes. Some of the most common benefits include:
- **Consistency across environments:** No more "It works on my machine" issues.
- **Isolation:** Docker containers keep apps and their dependencies separate from one another.
- **Portability:** Move applications between development, testing, and production seamlessly.
- **Efficiency:** Docker containers are lightweight and share system resources efficiently.
- **Scalability:** Easily scale applications to handle more users by creating additional containers.
- **DevOps integration:** Docker bridges the gap between development and operations teams, streamlining the workflow from coding to deployment.

## Key Concepts

Docker revolves around two main concepts: **images** and **containers**.

### Images
A **Docker image** is a lightweight, standalone package that includes everything needed to run a piece of software: the code, runtime, libraries, and system tools. You can think of a Docker image as a recipe for your application. 

### Containers
A **Docker container** is a runnable instance of a Docker image. It is the execution environment that contains the necessary components to run your app. You can create multiple containers from the same image, similar to having multiple servings of the same meal from a single recipe.

### Volumes and Networks
- **Volumes:** Persistent data storage that ensures data durability, even if a container is stopped or removed.
- **Networks:** Communication channels between Docker containers and the external world, enabling containers to share information and services while maintaining isolation.

## Basic Docker Workflow

Docker follows a workflow involving three main components:
- **Docker client:** The command-line tool or graphical interface you use to interact with Docker (e.g., `docker run`, `docker build`).
- **Docker host (Daemon):** The background process that manages images, containers, and tasks on the system.
- **Docker registry (Docker Hub):** A centralized repository where Docker images are stored, similar to GitHub for code. You can pull public images from Docker Hub or push your own images to share with others.

