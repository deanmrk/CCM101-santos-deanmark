# Laboratory 04 - The Cloud Native Engineer

## Mission Overview
for this lab, it focuses on understanding containerization and how Docker is used to deploy applications efficiently compared to traditional virtual machines.

## Objectives
- Understand the difference between Virtual Machines and Containers
- Use basic Docker commands
- Deploy an Nginx container
- Manage the container lifecycle

## Docker commands i executed
- docker --version
- docker pull nginx
- docker run -d -p 8080:80 nginx
- curl http://localhost:8080
- docker ps
- docker stop 8c0b086f586b <br>
- docker rm 8c0b086f586b <br>

## The Skills i learned
- Basic Docker commands and usage
- Deploying containers quickly
- Managing containers using CLI
- Understanding port mapping

## Challenges i encountered 
- Learning and remembering Docker commands at first
- Understanding how port mapping works (8080:80)
- Identifying container IDs when stopping and removing containers
