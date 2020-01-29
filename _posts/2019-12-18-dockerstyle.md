---
layout: post
title: dockerfile style guide
tags: docker container dockerfile dockerdecember
---

# dockerfile style guide

#### This will be a work in progress for some time

### Dockerfile Do's

- Follow the official [best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- Use staged builds
- One line per target/arg on provisioning commands (apt, pip, cmake)
- Avoid cache cruft with installers (`rm -rf /var/lib/apt/lists/*` for apt, `--no-cache-dir` for pip)
- Use `.dockerignore` and limit size of your docker context (I could do an entire post on this)
- Use [tini](https://github.com/krallin/tini) instead of `bash` for entrypoints
- Mount large assets (models, databases) rather than include in the image
- Split long lines with `\ `

### Dockerfile Don't's

- Put source code and build artifacts in the same parent dir
- Separate operations that add files and `rm` into separate `RUN` directives. 
  This creates bloat due to the way overlayfs works
- Use command-line flags in entrypoint for anything which might vary between deploys

### Interactive Container Dockerfile Don't's 

- Don't put anything in `/root` (or whatever is `$HOME` for app user) you are not willing 
    to mount-over
    - this facilitates things like mounting your `$HOME` into a named volume for persistence


### Exceptions
- Generally avoid adding any large assets to the image directly. However, if you do not
  control the deployment of the image, it may be adviseable to include these in your
  production image. If you do so, put them *before* any steps which copy in code that 
  changes frequently
- Use `pip install -e` (unless you are making an interactive/dev container)