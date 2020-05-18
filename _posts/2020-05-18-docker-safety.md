---
layout: post
title: How to get yourself hacked with Docker
tags:  cuda nvidia sm architecture caffe tensorflow pytorch
---

# Hacking yourself with Docker (and how to avoid pwnage)

I locked myself out of my desktop. I had changed the password for some reason, just before the
move. I didn't touch it for months, and when I came back to it, I couldn't remember what I 
had set it to. Luckily, I knew my dev laptop had ssh keys to it, and my main user had
docker permissions (good ol' `sudo usermod -aG docker $USER`). 

After sshing in, and some failed tutorials and a bit of experimentation with permissions,
I simply mounted a base ubuntu container with `-v /etc:/etc2`, shelled
into it, `mount --bind /etc2 /etc`, then `passwd mike` to reset my user password. 
Broke my keyring, but at least I got in. Yeah there are recover disk things but this was 
really fast. 

# Security in Layers

Until we get production-stable [rootless mode Docker daemon](https://docs.docker.com/engine/security/rootless/), 
bind mount attacks like this are still going to be possible, but we can mitigate aspects and build
layers of security. 

# Non-root USER

Starting at the image level, container images can be built with non-root USER for added security. 
The docker daemon still has root, but the UID of the user running in the container impacts how the kernel views that process. 
Containers are just an abstraction like namespaces, containerized processes are still just processes to the kernel. 
Let's say you accidentally mount `-v /etc:/etc`. If your UID in the container is the default `0`, 
you can touch this directory. However by creating a custom user and setting the `USER` directive, your process can't touch it.

There's a small caveat, if the docker user UID (or GID) matches your host user UID (default is 1000) OR a GID your user is in 
(like, if group docker is 999), then that process can touch your $HOME 
(I always mount -v $HOME:$HOME:ro but let's say you forgot. You can jam this with
```
RUN groupadd -r -g 23456 myuser && useradd -r -g myuser myuser -u 23456
```
Conversely, if you want to create a container which behaves like your host user, you can pass in your $UID, and 
allow your containerized process to have the same user/group behavior (instead of writing root-owned files into -v mounts)

