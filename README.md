# gitlab-setup

## Prerequeties:
 * direnv.
 * docker-compose.

## Things to change before running docker compose
* edit ``.envrc`` file and change the variable according to the needs.
* edit ``.env`` file to use the docker network.

## Command to run
``docker-compose up -d``

Above command does the following things:
* gitlab instance (container -> gitlab)
* gitlab runner (container -> gitlab-runner)

## Post gitlab and gitlab-installation(Register gitlab-runner to gitlab instance)
``sudo docker run --rm -it --net=<gitlab-instance-network> -v ${GITLAB_HOME}/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register``

While registering gitlab-runner to gitlab instance few things to keep in mind

1)Enter the gitlab instance url as: http://<gitlab-container-name>

once the registration done successfully.We have to make following changes in config.toml file

At root config:
concurrent=(4)Number of concurrent jobs that can be run by this runner

At runner-section:
clone_url=http://<gitlab-container-name>

At runner-docker section:
volumes= ["/var/run/docker.sock:/var/run/docker.sock"]
network_mode = "<gitlab-network>"

