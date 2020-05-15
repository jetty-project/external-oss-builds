# External Oss Builds

This repository contains some Jenkinsfile and other stuff to build opensource projects who use Jetty

The idea is to be able to build those projects with a staged release of Jetty or snapshot builds to test we are backward compatible

- `Jenkinsfile.airlift` build Airlift project https://github.com/airlift/airlift with jetty project version as parameter
- `Jenkinsfile.spring-boot` Build springboot https://github.com/spring-projects/spring-boot with jetty project as parameter

