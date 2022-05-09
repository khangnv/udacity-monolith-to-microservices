# Overview

This is a very simple, bare-bones NodeJS project created for you to use with Docker.

## Local Setup

**_Note_**: This is only needed if you want to run the app locally. You don't need to install the dependencies or run the server if you are running the code inside a Docker container.

- Install dependencies: `npm install`
- Run server: `node server.js`

## Container Setup

- Build image: `docker build .`
- Run container with image: `docker run {image_id}` where `image_id` can be retrieved by running `docker images` and found under the column `IMAGE ID`
- You can use the `-d` flag to run the container in the background. This will enable you to run other commands in your terminal while the container is running.

## Container Teardown

- Remove container: `docker kill {container_id}` where `container_id` can be retrieved by running `docker ps` and found under the column `CONTAINER ID`

## Notes

- Build and push the docker image to DockerHub.
- Create an new user with 'AdministratorAccess', 'AmazonEKSServicePolicy', 'AmazonEKSWorkerNodePolicy' permissions and allow to login AWS console.
- Login AWS Console with new user credentials.
- Following to #5 (Kubernetes on AWS) to create EKSClusterRole, NodeRole roles.
- Create EKS Cluster and EKS Node Group.

# Setup

- `aws configure` (with access_key, secret_key of new user)
- `aws sts get-caller-identity`
- Create or update a kubeconfig file for the cluster:
  `aws eks update-kubeconfig --region {region-code} --name {cluster-name}`
- Test the configuration:
  `kubectl get svc`

# Deploy resources

- `kubectl apply -f deployment.yaml`
- `kubectl apply -f service.yaml`

# Confirm resources

- Show the pods in the cluster:
  `kubectl get pods`
- Show the services in the cluster:
  `kubectl describe services`
- Display information about the cluster:
  `kubectl cluster-info`
- Get more metadata about the cluster:
  `kubectl cluster-info dump`

# Attach to a container in a pod:

- List out all pods:
  `kubectl get pods`
- Attach to the container of the pod:
  `kubectl exec -it {pod-name} sh`
- List out all files: `ls`
- Check the running processes inside the container:
  `ps aux`
- Quit the shell in the container:
  `exit`

# Horizontal Pod Autoscaler

- Create HPA:
  `kubectl autoscale deployment <DEPLOYMENT_NAME> --cpu-percent=<CPU_PERCENTAGE> --min=<MIN_REPLICAS> --max=<MAX_REPLICAS>`
- View HPA:
  `kubectl get hpa`
