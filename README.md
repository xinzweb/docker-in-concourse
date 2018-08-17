# Running Docker inside Concourse container
Example of how to run `dockerd` inside concourse pipeline.

You can find the example pipeline started `dockerd` inside a concourse task.

```bash
# deploy the pipeline
fly -t your-concourse set-pipeline -p test-docker-in-concourse -c pipeline.yml
```

Once you start your pipeline, and click on the job `docker in concourse`, you should
see `docker` works inside a concourse container.

# Behind the Scenes

- container has to be privileged in order to start `dockerd`
- `dind.bash`: setup scripts to run `dockerd`
- [`docker-image`](https://github.com/concourse/docker-image-resource) concourse resource
  is required to run a container from a docker image with `dockerd` installed
- The `dockerd` is fresh and doesn't have any cached images
