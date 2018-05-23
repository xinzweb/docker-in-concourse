# Running Docker inside Concourse container
Example of how to run `dockerd` inside concourse pipeline.

You can find the example pipeline started `dockerd` inside a concourse task.

```bash
# deploy the pipeline
fly -t your-concourse set-pipeline -p pipeline.yml
```

Once you start your pipeline, and click on the job `docker in concourse`, you should see `docker` works inside
a concourse container. You expect to see following output:

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
Unable to find image 'docker:latest' locally
latest: Pulling from library/docker
ff3a5c916c92: Pull complete
1a649ea86bca: Pull complete
ce35f4d5f86a: Pull complete
d0600fe571bc: Pull complete
e16e21051182: Pull complete
a3ea1dbce899: Pull complete
Digest: sha256:eb3f84220dfdb3d37cc5fdee03733fbe4a2c7935eebb5bd93c8f2db4c2b3b63d
Status: Downloaded newer image for docker:latest
bin    dev    etc    home   lib    media  mnt    proc   root   run    sbin   srv    sys    tmp    usr    var
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker              latest              2232c0bbbb8c        12 days ago         133MB
```

# Behind the Scenes

- container has to be privileged in order to start `dockerd`
- `dind.bash`: setup scripts to run `dockerd`
- [`docker-image`](https://github.com/concourse/docker-image-resource) concourse resource
  is required to run a container from a docker image with `dockerd` installed
- The `dockerd` is fresh and doesn't have any cached images
