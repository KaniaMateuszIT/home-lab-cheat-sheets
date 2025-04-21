# Docker

## Running Containers

| COMMAND                       | DESCRIPTION                                     |
|------------------------------|-------------------------------------------------|
| `docker run <image>`         | Start a new container from an image            |
| `docker run -it <image>`     | Start a new container in interactive mode      |
| `docker run --rm <image>`    | Start a new container and remove it when it exits |
| `docker create <image>`      | Create a new container                         |
| `docker start <container>`   | Start a container                              |
| `docker stop <container>`    | Graceful stop a container                      |
| `docker kill <container>`    | Kill (SIGKILL) a container                     |
| `docker restart <container>` | Graceful stop and restart a container          |
| `docker pause <container>`   | Suspend a container                            |
| `docker unpause <container>` | Resume a container                             |
| `docker rm <container>`      | Destroy a container                            |
