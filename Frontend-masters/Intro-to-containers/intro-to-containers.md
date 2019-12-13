# Complete intro to containers

## Details/Prerequesites

- 12/12/19
- Brian Holt
- [Course Repo](https://github.com/btholt/complete-intro-to-containers)

Notes/prerequesites with running containers:

- Very memory heavy. If you're running on a personal machine, better to have at least 8GB of RAM
- Bandwidth heavy when you're pulling images

## Intro: What are containers?

- In a nutshell, it's some of the core features of the Linux kernel "duct-taped" together
  - For more context on kernels, etc, check out the [Full stack eng for FE devs](https://frontendmasters.com/courses/fullstack-v2/) course.

### The progression to containers

"Bare Metal" = Literal Servers

- Zero abstractions; your code is executing on a literal machine somewhere
  - Good for performance
  - Caveat that someone physically has to be handling those servers
  - Physical presence means any and all changes have to go through the process of setting up and maintaining server infrastructure

### Virtual machines

- Next step

### Containers

- finally

## Crafting Containers By Hand (Building blocks of a container)

As previously stated, a container is just a few core linux kernel features stitched together.

We're going to build a container by hand and see how each of these work individually.

- Note: this is everything that docker does behind the scenes for you when a container is spun up.

### chroot

- chroot = "change root"
- Lets you set the root directory of a new process

Why is this a good thing?

- In the use case of containers, it lets us set the root directory wherever it should be for a given container
- Now the the new container's group of processes can't see outside of it, because you can't see outside the current root

Question: why was the first command not required to be copieed when I ran `ldd /bin/bash`?

- Answer: you only need to copy the ones that have full paths
  - (Brian didn't know the full reason for why that's the case)

### namespace

Namespaces protect processes.

### cgroups

Prevent runaway processes from taking down servers.

Example scenario: 2 isolated processes are running on the same server. If they both happen to start eating at resources simultaneously (or one is getting especially greedy), there runs the risk that the whole server could fall over

### Summary of building blocks

In a nutshell, a container has 3 core features of the linux kernel to accomplish some specific goals:

1. **chroot** = isolates a file system
2. **namespace** = isolates processes from other processes, networks, etc
3. **cgroups** = limit a tree of processes on what it can use (memory, CPU, etc)

## Docker

### Tags

`docker run -t node` implicitly runs `node:latest`

- In reality, there are _tons_ of [different tags](https://hub.docker.com/_/node/) for this.
- Gives you very fine-grained control over what version of something you're trying to run.

`docker run` = start a new container
`docker exec` = run a command on a currently running container

## Dockerfiles

So far, the focus has been on running containers with pre-existing images that we've gotten off of Dockerhub. Dockerfiles allow us to build _our own_ containers. All the stuff we're building now can be found in the [companion repo](https://github.com/btholt/projects-for-complete-intro-to-containers).

### Issue: I can't access my server via localhost! 😭

`docker run --init --publish 3000:8000 my-node-app`

`publish` lets you forward a port out of a container to the host computer. The syntax is `CONTAINER_PORT:LOCAL_PORT`. So in the above example, you can read that as "Navigating to the 3000 port on my machine forwards to 8000 on my container.

`docker run --rm container`

`--rm` Automatically removes a container once it exits

- Useful for cleaning up after yourself and not leaving old containers around

**PROTIP**: pipe JSON output in terminal to jq for colorized output
