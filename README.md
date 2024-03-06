ASP.NET Core Pipeline Deployment

Assumptions:
The following checklist should be completed before proceeding with the deployment:

1) A Kubernetes (k8s) cluster is available.
2) Persistent Volume Claim (PVC) with PVC claim exists.
3) You have the necessary permissions to manage resources in k8s using the .config file.
4) Git source code management (SCM) is set up with a repository and access credentials.
5) A repository is available to host the chart and Docker images, along with the necessary credentials.
6) The client machine has the required CLI tools installed, such as kubectl and Helm.
7) Custom JNLP agent image may need to be created to support Helm chart deployment on the agent.

Step-by-Step Implementation:

1) Clone the repository to your local machine or desired repository location.
2) Create a DevOps namespace in the Kubernetes cluster using the following command:
Command: kubectl apply -f namespace.yaml
3) Deploy the Jenkins instance on the Kubernetes cluster using Helm:
Command:``` helm upgrade --install devops -n devops jenkins/jenkins -f jenkins/custom_value.yaml```
4) Once Jenkins is up and running, log in and perform the following configurations:
- Login to Jenkins and go to <URL>//credentials/store/system/domain/_/.
- Define the following credentials:
- Git access credentials
- .config file credentials  (K8s config as file) 
- Docker/chart repository credentials
5) Create a pipeline job in Jenkins:
- Choose the pipeline type in Jenkins.
- In the pipeline section box, select "Pipeline script SCP".
- In SCP, choose Git as the source.
- Provide the SSH:/repo details.
- Attach the credentials you created for Git.
- Specify the branch path.
- Leave the default Jenkinsfile, as it will use the Jenkins file from the root directory.
6) Continue with the remaining steps as per your specific pipeline requirements.
