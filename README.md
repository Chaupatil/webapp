# webapp

Summary of Steps

1. I created a new repository on GitHub to host the source code and Kubernetes manifests for the application.

2. I installed Argo CD in my Kubernetes cluster by applying the official installation manifests. This involved creating the `argocd` namespace and deploying the Argo CD components.

3. I installed Argo Rollouts by applying the official installation manifests, which created the necessary Custom Resource Definitions (CRDs) and deployed the Argo Rollouts controller.

4. I created a `Dockerfile` to build a Docker image for the web application. I then built the image and pushed it to a container registry .i.e Dockerhub.

5. I created Kubernetes manifests for the application deployment and service, and modified them to use the Docker image I had pushed to the container registry. I then configured Argo CD to monitor my Git repository and automatically deploy the application to my Kubernetes cluster.

6. I modified the application deployment to use the `Rollout` resource provided by Argo Rollouts, and defined a canary release strategy in the rollout definition. I then triggered a rollout by updating the Docker image in the manifests and pushing the changes to my Git repository.

7. I used Argo Rollouts to monitor the progress of the canary release, ensuring that the new version was gradually rolled out and tested before proceeding with the complete deployment.

Challenges Encountered:

- Initially, I faced some issues with installing Argo Rollouts and its CRDs. I resolved this by double-checking the installation steps and ensuring that the CRDs were installed correctly.

- Accessing the Argo CD service through the `minikube service` command on my local machine was problematic, as I encountered connection reset issues. I troubleshot this by checking firewall settings, restarting the Minikube cluster, and ensuring that the `minikube tunnel` command was running correctly.

Clean Up

1. Delete the Argo CD and Argo Rollouts resources:

To Delete Argo CD resources - kubectl delete -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

To Delete Argo Rollouts resources - kubectl delete -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml

2. Delete the application resources:

To Delete the application deployment, service, and any other resources - kubectl delete -f "manifestsfile"

3. Delete the namespaces:

To Delete the argocd namespace - kubectl delete namespace argocd

To Delete the argo-rollouts namespace - kubectl delete namespace argo-rollouts

To Delete the namespace for web-app application - kubectl delete namespace web-app
