# Publish Image action

This actions is intended for publishing docker images either to a public registry, or private.

## Usage

### Workflow permissions
This action requires special permission at workflow level

#### Github

```yaml
permissions:
  content: read
  packages: write
```

#### ECR

```yaml
permisions:
  content: read
  id-token: write
```


### Inputs

|     input      | required | default value  | description                                                                                               |
| :------------: | :------: | :------------: | :-------------------------------------------------------------------------------------------------------- |
|  `image-name`  |  `true`  |      `""`      | The image name, in case of ECR it's the repository name                                                   |
|   `context`    | `false`  |      `.`       | The context path for the docker build                                                                     |
| `docker-file`  | `false`  | `./Dockerfile` | The path to the Dockerfile to build                                                                       |
| `github-token` | `false`  |      `""`      | Required only when registry is `github`                                                                   |
|   `registry`   | `false`  |    `github`    | The registry location. Either `github` or `ecr`                                                           |
|    `prefix`    | `false`  |      `""`      | Prefix to be appended to the image tag, for example `branch-` will result on `<image-name>:branch-master` |

## Examples

### Publish image to github packages

```yaml
- name: Build and publish
  uses: littlehorse-enterprises/publish-image@v1
  with:
    image-name: <image-name>
    dockerfile: path/to/Dockerfile
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

### Publish image to ECR

```yaml
- name: Build and publish
  uses: ittlehorse-enterprises/publish-image@v1
  with:
    image-name: <image-name>
    dockerfile: path/to/Dockerfile
    registry: ecr
```

### Adding image prefix

```yaml
- name: Build and publish
  uses: ittlehorse-enterprises/publish-image@v1
  with:
    image-name: <image-name>
    dockerfile: path/to/Dockerfile
    prefix: brach-
```
