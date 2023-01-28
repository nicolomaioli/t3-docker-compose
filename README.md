# Create T3 App - Docker Compose example

This is a [T3 Stack](https://create.t3.gg/) project bootstrapped with
`create-t3-app`.

This example shows how to:

- Spin up a `mysql` while running the application with `npm run dev`;
- Provides a bare-bones setup for [Visual Studio Code Remote Containers](https://code.visualstudio.com/docs/devcontainers/containers)
- Sping up a production build of the application alongside a `mysql` database
  in a single `docker compose` stack, running locally.

Tested on the following environment:

```
OS: Fedora Linux 37 (Workstation Edition) x86_64
Kernel: 6.1.6-200.fc37.x86_64
CPU: AMD Ryzen 7 PRO 6850U with Radeon Graphics (16) @ 2.700GHz
Memory: 4271MiB / 30846MiB
```

Docker info:

```
Client: Docker Engine - Community
 Version:           20.10.23
 API version:       1.41
 Go version:        go1.18.10
 Git commit:        7155243
 Built:             Thu Jan 19 17:34:54 2023
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.23
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.18.10
  Git commit:       6051f14
  Built:            Thu Jan 19 17:32:33 2023
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.15
  GitCommit:        5b842e528e99d4d4c1686467debf2bd4b88ecd86
 runc:
  Version:          1.1.4
  GitCommit:        v1.1.4-0-g5fd4c4d
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0

Docker Compose version v2.15.1
```

If you are using Docker Desktop on MacOs or Windows, Apple Silicon, WSL, etc.
your mileage might vary, however some effort has been put in ensuring
compatibility with Apple Silicon.

## Develop

The development workflow looks like:

```sh
npm install

# spin up the mysql database
npm run compose:up

# push db changes
npm run prisma:push

# develop the application locally taking advantage of HMR etc.
npm run dev

# kill the stack
npm run compose:down
```

## Visual Studio Code Remote Containers

This is a bare-bones example with the following features and limitations:

- Using the same `Dockerfile` as your production build;
- Targets the `devcontainer` stage;
- Runs as `root`:
  - Adding a non-root user depends in part on your dev environment, see
  [Add a non-root user to a container](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user);
- Using the same base `docker-compose.yml` as everything else;
- Does not include any extensions or tools, with `git` offered as an example;
- Runs `npm ci` and `npm run prisma:push` automatically on startup;
- Exposes the following ports to localhost:
  - `3306`: to access MySQL;
  - `5555`: to access Prisma Studio;
  - `8080`: to access the application.

Open the repository in Visual Studio Code, install the recommended extension,
then accept the prompt or `ctrl+Shift+p` (`cmd+Shift+p` on Mac) and run
`Dev Containers: Rebuild Without Cache and Reopen in Container`.

Workflow:

```sh
# develop the application
npm run dev

# visit the application at localhost:8080

# run prisma studio
npm run prisma:studio

# visit prisma studio at localhost:5555

# push db changes
npm run prisma:push
```

## Run production build

To check the production build, either locally or in a CI environment, run:

```sh
# spin up a docker-compose stack with both the database and a prod build of the
# application. Note that this will share the same volume as spinning up the db
# only, devising a strategy to run migrations or push changes is your
# responsibility. Also note that this will build the application every time.
npm run compose:local:up

# visit the application at localhost:8080

# kill the stack
npm run compose:local:down
```
