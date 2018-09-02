# Container
## Instructions
### Dockerfile
*This guide is not dependent on Docker. If you are using Docker, there are general recommendations that **SHOULD** be applied to your microservice.*

Follow the [Docker Docs](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) for Dockerfile best practices

A container can accept input and write output (like a traditional function) or stream output (e.g., web servers, chatbots, social media streams).

* Keep images to a bare minimum
    * Consider using a parent image from `alpine` or a base image `FROM scratch`
* Include an `EXPOSE` instruction for external access
* Include an `ENTRYPOINT`
