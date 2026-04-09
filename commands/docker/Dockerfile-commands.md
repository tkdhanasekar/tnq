**comprehensive list of Dockerfile instructions (commands)** with **detailed explanations, syntax, behavior, and examples**.

---

# 1. `FROM`

### Purpose

Defines the **base image** for your Docker image.

### Syntax

```
FROM <image>[:tag] [AS <alias>]
```

### Explanation

* Must be the **first instruction** in most Dockerfiles.
* Can be used multiple times for **multi-stage builds**.
* Defines the starting filesystem.

### Examples

```
FROM ubuntu:22.04
FROM node:18
FROM python:3.11-slim
FROM nginx:latest
FROM golang:1.22 AS builder
FROM ubuntu:22.04
FROM node:18
FROM python:3.11
FROM nginx:latest
FROM alpine:3.19
FROM golang:1.22
FROM openjdk:17
FROM mysql:8
FROM redis:7
FROM scratch (empty base)
```

---

# 2. `RUN`

### Purpose

Executes commands during the image build process.

### Syntax

```
RUN <command>
RUN ["executable", "param1", "param2"]
```

### Explanation

* Each `RUN` creates a new **layer**.
* Used for installing packages, compiling code, etc.

### Examples

```
RUN apt update
RUN apt install -y curl
RUN mkdir /app
RUN pip install flask
RUN npm install
RUN apt update
RUN apt install -y curl
RUN mkdir /app
RUN pip install flask
RUN npm install
RUN useradd myuser
RUN chmod +x script.sh
RUN apk add --no-cache git
RUN echo "hello" > file.txt
RUN rm -rf /var/lib/apt/lists/*
```

---

# 3. `CMD`

### Purpose

Specifies the **default command** to run when a container starts.

### Syntax

```
CMD ["executable", "param1"]
CMD command param1
```

### Explanation

* Only one `CMD` is allowed (last one wins).
* Can be overridden using `docker run`.

### Examples

```
CMD ["python", "app.py"]
CMD ["nginx", "-g", "daemon off;"]
CMD node server.js
CMD ["sleep", "100"]
CMD ["bash"]
CMD ["node", "server.js"]
CMD ["nginx", "-g", "daemon off;"]
CMD ["bash"]
CMD ["sleep", "100"]
CMD ["redis-server"]
CMD ["java", "-jar", "app.jar"]
CMD ["./start.sh"]
CMD ["top"]
CMD ["echo", "Hello"]
```

---

# 4. `ENTRYPOINT`

### Purpose

Defines a **fixed executable** that always runs.

### Syntax

```
ENTRYPOINT ["executable", "param"]
```

### Explanation

* Unlike `CMD`, it **cannot be overridden easily**.
* Often combined with `CMD`.

### Examples

```
ENTRYPOINT ["python"]
ENTRYPOINT ["nginx"]
ENTRYPOINT ["/bin/bash"]
ENTRYPOINT ["java", "-jar", "app.jar"]
ENTRYPOINT ["docker-entrypoint.sh"]
ENTRYPOINT ["python"]
ENTRYPOINT ["node"]
ENTRYPOINT ["nginx"]
ENTRYPOINT ["bash"]
ENTRYPOINT ["sh", "-c"]
ENTRYPOINT ["java", "-jar", "app.jar"]
ENTRYPOINT ["./entrypoint.sh"]
ENTRYPOINT ["sleep"]
ENTRYPOINT ["redis-server"]
ENTRYPOINT ["top"]
```

---

# 5. `WORKDIR`

### Purpose

Sets the working directory inside the container.

### Syntax

```
WORKDIR /path
```

### Explanation

* Automatically creates directory if not exists.
* Affects `RUN`, `CMD`, `COPY`, etc.

### Examples

```
WORKDIR /app
WORKDIR /usr/src/app
WORKDIR /var/www
WORKDIR /home/user/project
WORKDIR /opt/service
WORKDIR /app
WORKDIR /usr/src/app
WORKDIR /home/user
WORKDIR /var/www
WORKDIR /opt/project
WORKDIR /data
WORKDIR /code
WORKDIR /workspace
WORKDIR /srv/app
WORKDIR /root/app
```

---

# 6. `COPY`

### Purpose

Copies files from host to container.

### Syntax

```
COPY <src> <dest>
```

### Explanation

* Only copies from local build context.
* Preferred over `ADD` for simple copying.

### Examples

```
COPY . /app
COPY package.json /app
COPY src/ /app/src/
COPY index.html /usr/share/nginx/html/
COPY requirements.txt /app/
COPY . /app
COPY app.py /app/
COPY requirements.txt /app/
COPY src/ /app/src/
COPY config.json /etc/config.json
COPY script.sh /usr/local/bin/
COPY .env /app/.env
COPY package.json /app/
COPY static/ /var/www/html/
COPY logs/ /var/log/app/
```

---

# 7. `ADD`

### Purpose

Similar to `COPY`, but with extra features.

### Syntax

```
ADD <src> <dest>
```

### Explanation

* Can extract tar files automatically.
* Can download from URLs (not recommended).

### Examples

```
ADD app.tar.gz /app
ADD https://example.com/file.txt /tmp
ADD . /app
ADD archive.zip /data
ADD config/ /etc/config/
ADD file.tar.gz /app/
ADD https://example.com/file.txt /app/
ADD app/ /app/
ADD archive.zip /data/
ADD config/ /etc/config/
ADD script.sh /usr/bin/
ADD . /app
ADD image.png /assets/
ADD backup.tar /backup/
ADD data/ /var/data/
```

---

# 8. `EXPOSE`

### Purpose

Declares container ports.

### Syntax

```
EXPOSE <port>
```

### Explanation

* Informational only (does not publish ports).
* Used by `docker run -p`.

### Examples

```
EXPOSE 80
EXPOSE 443
EXPOSE 8080
EXPOSE 3000
EXPOSE 5000
EXPOSE 6379
EXPOSE 3306
EXPOSE 27017
EXPOSE 9000
EXPOSE 22
```

---

# 9. `ENV`

### Purpose

Sets environment variables.

### Syntax

```
ENV key=value
```

### Explanation

* Available during build and runtime.

### Examples

```
ENV NODE_ENV=production
ENV PORT=3000
ENV PATH=/usr/local/bin:$PATH
ENV JAVA_HOME=/usr/lib/jvm/java-17
ENV APP_ENV=dev
ENV APP_ENV=production
ENV DEBUG=true
ENV PATH=/usr/local/bin:$PATH
ENV DB_HOST=localhost
ENV DB_USER=root
ENV DB_PASS=secret
ENV NODE_ENV=development
ENV JAVA_HOME=/usr/lib/jvm/java-17
ENV LANG=C.UTF-8
```

---

# 10. `ARG`

### Purpose

Defines build-time variables.

### Syntax

```
ARG name[=default]
```

### Explanation

* Only available during build.
* Not persisted in final image.

### Examples

```
ARG VERSION=1.0
ARG USERNAME
ARG PORT=8080
ARG BUILD_ENV=prod
ARG BASE_IMAGE=ubuntu
ARG VERSION=1.0
ARG PORT=8080
ARG USER=appuser
ARG ENV=dev
ARG BASE_IMAGE=ubuntu
ARG BUILD_DATE
ARG APP_NAME=myapp
ARG DEBUG=false
ARG API_URL
ARG NODE_VERSION=18
```

---

# 11. `VOLUME`

### Purpose

Creates a mount point for persistent storage.

### Syntax

```
VOLUME ["/data"]
```

### Explanation

* Data stored outside container lifecycle.

### Examples

```
VOLUME /data
VOLUME /var/lib/mysql
VOLUME /app/logs
VOLUME /config
VOLUME /backup
VOLUME /tmp/data
VOLUME /var/www/html
VOLUME /opt/storage
VOLUME /usr/share/nginx/html
VOLUME /mnt/data
```

---

# 12. `USER`

### Purpose

Specifies user to run commands.

### Syntax

```
USER <username>
```

### Explanation

* Improves security by avoiding root.

### Examples

```
USER root
USER appuser
USER 1000
USER nginx
USER nobody
USER www-data
USER postgres
USER mysql
USER node
USER daemon
```

---

# 13. `LABEL`

### Purpose

Adds metadata to image.

### Syntax

```
LABEL key=value
```

### Explanation

* Used for documentation and automation.

### Examples

```
LABEL version="1.0"
LABEL maintainer="admin@example.com"
LABEL description="Web app"
LABEL stage="production"
LABEL org.opencontainers.image.source="repo-url"
LABEL description="My App"
LABEL author="DevOps Team"
LABEL env="production"
LABEL release="stable"
LABEL project="docker-demo"
LABEL company="XYZ"
LABEL license="MIT"
LABEL stage="testing"
```

---

# 14. `ONBUILD`

### Purpose

Triggers instruction when image is used as base.

### Syntax

```
ONBUILD <instruction>
```

### Explanation

* Useful for base images.

### Examples

```
ONBUILD COPY . /app
ONBUILD RUN npm install
ONBUILD ADD . /src
ONBUILD RUN make build
ONBUILD CMD ["python", "app.py"]
ONBUILD RUN pip install -r requirements.txt
ONBUILD WORKDIR /app
ONBUILD ENV APP_ENV=prod
ONBUILD EXPOSE 3000
ONBUILD CMD ["node", "app.js"]
ONBUILD USER appuser
ONBUILD RUN make build
```

---

# 15. `STOPSIGNAL`

### Purpose

Defines system call signal for stopping container.

### Syntax

```
STOPSIGNAL signal
```

### Examples

```
STOPSIGNAL SIGTERM
STOPSIGNAL SIGKILL
STOPSIGNAL SIGINT
STOPSIGNAL SIGQUIT
STOPSIGNAL 9

```

---

# 16. `HEALTHCHECK`

### Purpose

Checks container health.

### Syntax

```
HEALTHCHECK CMD <command>
```

### Explanation

* Docker monitors container status.

### Examples

```
HEALTHCHECK CMD curl -f http://localhost || exit 1
HEALTHCHECK CMD wget --spider http://localhost
HEALTHCHECK CMD pg_isready
HEALTHCHECK CMD mysqladmin ping
HEALTHCHECK CMD echo "ok"
HEALTHCHECK CMD ping -c 1 localhost
HEALTHCHECK CMD exit 0
HEALTHCHECK CMD test -f /app/app.py
HEALTHCHECK CMD nc -z localhost 80
HEALTHCHECK CMD ps aux
HEALTHCHECK CMD curl -f http://localhost:3000/health
HEALTHCHECK CMD cat /proc/1/status
HEALTHCHECK NONE
```

---

# 17. `SHELL`

### Purpose

Overrides default shell.

### Syntax

```
SHELL ["executable", "parameters"]
```

### Examples

```
SHELL ["/bin/bash", "-c"]
SHELL ["powershell", "-Command"]
SHELL ["cmd", "/S", "/C"]
SHELL ["/bin/sh", "-c"]
SHELL ["/usr/bin/bash", "-c"]
SHELL ["powershell", "-Command"]
SHELL ["cmd", "/S", "/C"]
SHELL ["/bin/ash", "-c"]
SHELL ["/usr/bin/bash", "-c"]
SHELL ["/bin/zsh", "-c"]
SHELL ["pwsh", "-c"]
SHELL ["/busybox/sh", "-c"]
SHELL ["/usr/bin/env", "bash", "-c"]
```

---

# 18. `MAINTAINER` (Deprecated)

### Purpose

Specifies image author.

### Syntax

```
MAINTAINER name
```

### Explanation

* Replaced by `LABEL`.

### Examples

```
MAINTAINER John Doe
MAINTAINER admin@example.com
MAINTAINER Dev Team
MAINTAINER Ops Team
MAINTAINER Company Inc.

```

---

# Summary Table

| Instruction | Purpose                   |
| ----------- | ------------------------- |
| FROM        | Base image                |
| RUN         | Execute commands          |
| CMD         | Default container command |
| ENTRYPOINT  | Fixed executable          |
| WORKDIR     | Set working directory     |
| COPY        | Copy files                |
| ADD         | Copy + extra features     |
| EXPOSE      | Declare ports             |
| ENV         | Environment variables     |
| ARG         | Build-time variables      |
| VOLUME      | Persistent storage        |
| USER        | Set user                  |
| LABEL       | Metadata                  |
| ONBUILD     | Trigger instruction       |
| STOPSIGNAL  | Stop signal               |
| HEALTHCHECK | Health monitoring         |
| SHELL       | Change shell              |
| MAINTAINER  | Deprecated metadata       |

