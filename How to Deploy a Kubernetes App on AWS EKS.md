
<img width="1536" height="1024" alt="cover-awscommunity" src="https://github.com/user-attachments/assets/c5eb8846-d001-41d1-9e6c-dc4d17750fa0" />



AWS makes it much easier to deploy containerized applications. Running Kubernetes in the cloud is a powerful way to scale and manage these apps. Among the many managed Kubernetes services that AWS provides, Amazon EKS (Elastic Kubernetes Service) stands out for its seamless integration with the AWS ecosystem, strong reliability, and excellent support.
If you’re ready to move beyond local setups and want to deploy a real-world Kubernetes app on AWS EKS, this guide will walk you through the entire process. Whether you’re working on a microservice, a full-stack app, or just experimenting with Kubernetes in an environment that mimics production, you’ll find this walkthrough useful.
In this article, I’ll guide you through the process of creating your EKS cluster, deploying your application, and making it accessible over the internet, step by step.

## Prerequisites

To get started, make sure you have the following installed on your local machine, i.e., your laptop
 
- Have a basic understanding of cloud services.
-  Have a basic understanding of the Linux command line.
-  Have an [AWS account](https://aws.amazon.com/free/?gclid=Cj0KCQiAvvO7BhC-ARIsAGFyToVguvjmSCa99VkB7XsHepginSELSYCCYnVzZXeZSKFpRRTC8DKyh98aAkZkEALw_wcB&trk=2d3e6bee-b4a1-42e0-8600-6f2bb4fcb10c&sc_channel=ps&ef_id=Cj0KCQiAvvO7BhC-ARIsAGFyToVguvjmSCa99VkB7XsHepginSELSYCCYnVzZXeZSKFpRRTC8DKyh98aAkZkEALw_wcB:G:s&s_kwcid=AL!4422!3!645125273261!e!!g!!aws!19574556887!145779846712&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all).
-  Install eksctl, a simple CLI tool to create and manage EKS clusters.
-  Install kubectl, the standard Kubernetes command-line tool.
-  Install Docker to build and package your app into a container.

Before we set up a Kubernetes cluster for our application, it’s important to understand a few basic concepts.

## What is a Kubernetes cluster?
A Kubernetes cluster, also called K8S, is made up of machines (called nodes) that run containerised applications. It works alongside container engines like [CRI-O](https://cri-o.io/#what-is-cri-o) or [containerd](https://containerd.io/) to help you deploy and manage your apps more efficiently.
Kubernetes nodes come in two main types:
1. Master nodes (control plane): These handle the brainwork like scheduling, scaling, and managing the cluster’s overall state.
2. Worker nodes (data plane): They run the actual applications inside containers.
If you're new to Kubernetes or want to brush up, check out the free course [Introduction to Kubernetes (LFS158) ](https://training.linuxfoundation.org/training/introduction-to-kubernetes/?lid=axmt8lvbjbl8)from the Linux Foundation.

## What is Amazon Elastic Kubernetes Service?

Amazon Elastic Kubernetes Service (EKS) is a managed service that simplifies running Kubernetes on AWS without the need to set up or maintain your own Kubernetes control plane node. AWS EKS handles the complex tasks by managing the control plane, performing upgrades, and installing core components such as the container runtime and essential Kubernetes processes. It also provides built-in tools for scaling, high availability, and backups. With EKS, you or your team can focus on developing and deploying applications, while AWS takes care of the underlying infrastructure.

## Why Use Amazon EKS for Kubernetes?
Some key benefits of using AWS EKS:

- EKS manages upgrades, patching, and high availability for you, providing a fully managed control plane with minimal manual effort.
- You can easily scale your applications, and the infrastructure expands as your needs grow.
- Built-in support for IAM roles, private networking, and encryption.
- AWS EKS runs on highly available infrastructure across multiple AWS Availability Zones, ensuring your application remains accessible worldwide.
- With Amazon EKS, you gain the power of Kubernetes without the need to manage the underlying setup. This allows you to focus on building and running your applications.

## How do I create a Kubernetes cluster using AWS?


![let get started](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0gub3de51503dk0ly7vv.png)

### Step 1: Installing the Tools Needed to Create a Cluster
The easiest and most developer-friendly way to spin up an Elastic Kubernetes Service that will be used at the production level is by using eksctl. It takes care of much of the manual setup and automatically provisions the necessary AWS resources.
Before we begin, we need to install two essential tools:
- **eksctl**—This is used to create and manage your EKS cluster.
- **kubectl**—This allows you to interact with your cluster, deploy apps, and manage Kubernetes resources.
These tools will make it easy to set up your Kubernetes cluster and work with it directly from your terminal.

**How to Install eksctl**

- Open your browser and go to the official [eksctl documentation](https://eksctl.io/).
- Scroll down to the Installation section.
- Scroll to the Unix instructions if you're using Ubuntu or a similar system.
- Copy the installation command and paste it into your terminal.

![installing eksctl](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cv7hzy8f9jy4khbj3kgc.gif)

- Once it’s done, run `eksctl version` or `eksctl` to confirm the installation was successful.


![checking eksctl](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fama0vemtxv1j49znonv.gif)

## How to Install kubectl

The next step is to install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/). You can find the installation instructions in the official Kubernetes documentation, which provides steps based on your operating system.

```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

## Step 2: How to Create the Elastic Kubernetes Service (EKS) Cluster

Now that you've installed the tools needed to create and interact with a Kubernetes cluster on AWS, it's time to launch the cluster.

To get started, open your terminal and run the following command:

```
# Create an EKS cluster named "k8s-example" in eu-west-2 (London)
eksctl create cluster --name k8s-example --region eu-west-2   
```

![Creating a cluster](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qko6ox356ctfdwb0p9qc.gif)

One great thing about using AWS EKS is that once your Kubernetes cluster is created, it automatically updates your `~/.kube/config `file. This means you can start interacting with your cluster right away, using `kubectl` – no extra setup needed.


![.kube config created](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mqmyk2yj09o0uw25modl.png)

After running the command (as shown in the GIF above), your Kubernetes cluster is successfully created.


![GUI of AWS EKS](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wmra29y1ufaqk7egx198.gif)

Head over to the AWS console, and you’ll see your new cluster listed with a status of **Active**.

With your cluster up and running, it’s time to test the connection. You can do this by running a few kubectl commands in your terminal to list the nodes, pods and namespaces in your cluster.

**To test the connection:**

```
kubectl get nodes
```

This command lists all the nodes in your cluster.

```
kubectl get pods
```
This command lists all the pods currently running.

```
kubectl get namespaces
```
This command lists all the namespaces currently running.


![The test commands](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ertmjmwbf7yrt0rv79ui.png)

If each command returns a list of resources, congratulations! Your connection to the Kubernetes cluster is successful.

## Step 3: How to Create Kubernetes Manifests
Let’s define the application using a YAML file. In this file, you’ll create two key resources: a Deployment and a Service.

- The Deployment ensures your application runs reliably by specifying how many replicas to run, which container image to use, and how to manage updates.

- The Service makes your application accessible — both within the Kubernetes cluster and, if needed, from the internet, even if the underlying pods change or restart.
Together, these resources orchestrate your application so it can run consistently in different environments and be accessed by others.

```
#deployment-example.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: amazon-deployment
  namespace: default
  labels:
    app: amazon-app
spec:
  replicas: 5
  selector:
    matchLabels:
      app: amazon-app
      tier: frontend
      version: 1.0.0
  template:
    metadata:
      labels:
        app: amazon-app
        tier: frontend
        version: 1.0.0
    spec:
      containers:
        - name: amazon-container
          image: ooghenekaro/amazon:2
          ports:
            - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: amazon-service
  labels:
    app: amazon-app
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 3000
  selector:
    app: amazon-app
```
The service uses a LoadBalancer type, which tells AWS to provision an `Elastic Load Balancer (ELB)` and route traffic to the pods.

## Step 4: How to Deploy the App to EKS
Now that your YAML file is defined and the Kubernetes cluster on AWS EKS is ready, it’s time to deploy your application.

To do this, run the following command in your terminal to apply the configuration defined in your manifest file:

`kubectl apply -f deployment-example.yaml`
This command tells Kubernetes to create the necessary pods and services based on what’s specified in the manifest file.

Next, you can check the status of your pods and services:

```
kubectl get pods
kubectl get svc or service
kubectl get all
```

![getting all the resource](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c6dcpg4gatsi748fwygy.png)

## Step 5: How to Access Your Application
To view your application in the browser, run the following command to list your services:

```
kubectl get svc
```
Look for the EXTERNAL-IP of your service.


![exposing the external IP](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0umflxeiw86q5l765n98.png)

Copy the IP address and paste it into your browser. Your app should now be live!


![The live app](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h8rmzmrnvzgv5prg06js.png)

## Conclusion
Deploying a Kubernetes app on AWS EKS may seem complex at first, but with tools like eksctl and kubectl, the process is surprisingly approachable.

Whether you're a developer experimenting with Kubernetes or a team looking to scale production workloads, EKS provides a strong, scalable foundation that supports your applications as they grow.

## Resources

- If you’d like to continue this step-by-step Kubernetes, you can find the full version here: [How to Deploy and Scale Kubernetes Apps on AWS EKS](https://ijtechguide.gumroad.com/l/hhqiv)

- [Play with Kubernetes](https://labs.play-with-k8s.com/)

- [Docker 101 Tutorial](https://www.docker.com/101-tutorial/)

- [How to Create a CI/CD Pipeline Using AWS Elastic Beanstalk](https://dev.to/ijay/how-to-create-a-cicd-using-aws-elastic-beanstalk-15nh)

Thanks for reading!

