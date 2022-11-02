# Github action to build docker image

Shared build steps for Odyssey projects to build a docker image from a github repositry.

This generates a version based on git branch or tag.
Builds a docker image, using the repositories Dockerfile.
Pushes and tags the image, with git commit hash and the generated version.
If it's a tagged version (vX.Y.Z), an action event is dispatched to the Operations repository to prepare a release to acc environment.


## Usage

```yml
      - id: build
        uses: OdysseyMomentumExperience/docker-build-action@v1
        with:
          registry-server: ${{ secrets.REGISTRY_LOGIN_SERVER }}
          registry-user: ${{ secrets.REGISTRY_USERNAME }}
          registry-pass: ${{ secrets.REGISTRY_PASSWORD }}
          npm-token: ${{ secrets.NPM_TOKEN }}
```

### Inputs
| Name | Description | Default |
| --- | --- | --- |
| `image-name` | Name of the created docker image | The name of the repository |
| `registry-server` | (**required**) Docker registry location/URL |  |
| `registry-user` | (**required**) Docker registry username for authentication |  |
| `registry-pass` | (**required**) Docker registry password for authentication |  |
| `npm-token` | Github access token (PAT) to access private npm packages |  |
| `multistage-target` | Docker build target for multistage builds.  |  |
| `extra-args` | Additional arguments added to the docker build call.  |  |

### Outputs
| Name | Description |
| --- | --- |
| `version` | The generated version string, e.g. 'v1.2.3' or 'latest' |
