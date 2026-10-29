# Docker Interview Preparation: Scenario-Based Questions

## Section 1: Docker Fundamentals

1.  Your Spring Boot application works on your laptop but fails on
    another developer's machine. How would you solve this?
2.  You have built one Spring Boot image, but your application needs
    three instances to handle requests.
3.  What happens when you stop and remove a container?
4.  You need to check whether your container is running. How do you
    investigate it?

## Section 2: Dockerfile and Image Building

1.  Your Docker image is very large. How would you reduce its size?
2.  Every small code change makes your Docker build slow. What would you
    do?
3.  What is the difference between `CMD` and `ENTRYPOINT`?
4.  Your Docker build fails because the JAR file cannot be found. How do
    you fix it?
5.  What is the difference between `COPY` and `ADD`?
6.  What is a Docker build context, and why does `.dockerignore` matter?

## Section 3: Ports and Networking

1.  Your container is running, but you cannot access the application
    from your browser. What will you check?
2.  Explain bridge networking using a real-time example.
3.  Why does `localhost` fail when one container connects to another?
4.  Explain Docker port mapping versus `EXPOSE`.
5.  What are bridge, host, none, and overlay networks?

## Section 4: Volumes and Persistent Data

1.  Your PostgreSQL container is deleted. How can you prevent database
    data loss?
2.  What is the difference between a named volume and a bind mount?
3.  What is the difference between a volume and the container writable
    layer?

## Section 5: Environment Variables, Configuration, and Security

1.  How do you pass environment-specific configuration to Docker?
2.  A developer hardcoded a database password in a Dockerfile. What is
    the problem?
3.  How do you secure a Docker container?

## Section 6: Docker Compose and Multi-Container Applications

1.  Your application requires Spring Boot, PostgreSQL, and Redis. How
    would you run all three?
2.  What is the difference between `docker compose up` and
    `docker compose down`?
3.  Your backend starts before the database is ready and fails. How
    would you fix it?
4.  Can Docker Compose replace Kubernetes?

## Section 7: Docker Registries and Image Versioning

1.  You built an image locally. How do you deploy it on another machine?
2.  Why should you avoid using `latest` as your production image tag?
3.  Docker image pull fails with an authentication error. What will you
    check?

## Section 8: Docker Logging, Monitoring, and Debugging

1.  Your application is running inside a container, but you cannot find
    its logs.
2.  Your Docker container consumes too much CPU or memory. How do you
    investigate?
3.  A container keeps restarting. How do you identify the root cause?
4.  What are Docker restart policies?

## Section 9: Health Checks and Graceful Shutdown

1.  How do you know whether a Docker container's application is actually
    healthy?
2.  Your Spring Boot application is terminated while processing
    requests. How do you handle graceful shutdown?

## Section 10: Docker and CI/CD

1.  How would you automate Docker deployment through a CI/CD pipeline?
2.  A deployment works in testing but fails in production. How would
    Docker help you investigate?

## Section 11: Advanced Docker Interview Scenarios

1.  What is the difference between Docker Engine and a container
    runtime?
2.  What is a dangling image, and how do you clean up unused Docker
    resources?
3.  How do you troubleshoot Docker DNS or network connectivity problems?
4.  How do you pass build-time arguments versus runtime configuration?
5.  What happens when a Docker container uses too many file descriptors
    or processes?
6.  Why should you use immutable image versions in production?

## Section 12: Additional Docker Concepts You Should Not Miss

1.  What happens if the Docker daemon stops?
2.  What is the difference between Docker Swarm and Kubernetes?
3.  How would you build a multi-architecture Docker image?
4.  How would you prevent a container from running as root?
5.  What is the difference between Docker container health and
    application availability?
