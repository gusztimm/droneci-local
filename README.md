# About
This is a local deployment of Drone CI for executing CI/CD pipelines locally, without consuming cloud resources. This document shows how to implement Drone for a GitHub repository.

# Prerequisites

1. Setup public domain name

When installing the Drone server on your laptop for testing purposes, use a service like `ngrok` to provide your Drone server with a publicly accessible domain name.

After having registered on `ngrok`, install on your local machine and add your token, finally start with:

```
ngrok http --domain=heroic-gator-choice.ngrok-free.app 8080
```

Note that standard ports might interfere with other services already listening, like Kubernetes Ingress Controllers. Therefore, you might want to especially avoid using `80` and `443`.

See https://dashboard.ngrok.com/get-started/setup/windows for detailed instructions.

2. Register GitHub OAuth application

Create a GitHub OAuth application. The Consumer Key and Consumer Secret are used to authorize access to GitHub resources.

See https://docs.drone.io/server/provider/github/ for details.

3. Fill out env files

There are example env files shipped with this repository, fill in and rename as follows.

'drone-server.env': Env file for the Drone Server
'drone-runner.env': Env file for the Drone Runner

# Deployment

### Using Docker Compose

Fire up the Drone environment using:

```
docker compose up
```

### Verification

The server should log something like `{"acme":false,"host":"heroic-gator-choice.ngrok-free.app","level":"info","msg":"starting the http server","port":":80","proto":"http","time":"2024-06-29T12:06:10Z","url":"http://heroic-gator-choice.ngrok-free.app"}`

The runner should log `msg="successfully pinged the remote server"`.

# Usage

Visit the domain that you have mapped (e.g., https://heroic-gator-choice.ngrok-free.app) and authenticate to your GitHub account.

`.drone.yml` file should be present in each repository that you want to build pipelines for.

If you fork this repo, make sure not to include your GitHub secrets in your commits :)
