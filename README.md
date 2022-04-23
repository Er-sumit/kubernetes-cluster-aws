### https://kubernetes.io/docs/setup/production-environment/tools/kops/
# Installing Kubernetes with kops
This quickstart shows you how to easily install a Kubernetes cluster on AWS. It uses a tool called kops.

kops is an automated provisioning system:

Fully automated installation
Uses DNS to identify clusters
Self-healing: everything runs in Auto-Scaling Groups
Multiple OS support (Debian, Ubuntu 16.04 supported, CentOS & RHEL, Amazon Linux and CoreOS) - see the images.md
High-Availability support - see the high_availability.md
Can directly provision, or generate terraform manifests - see the terraform.md
Before you begin

You must have kubectl installed.
``` curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl" ```

Then follow
``` mkdir -p bin; mv kubectl bin/.; chmod +x bin/kubectl; export PATH=$PATH:/Users/w/Desktop/MyWork2022/Django_RestAPIs_Serializer_Project_2022/AWS/bin; kubectl version --client```

You must install kops on a 64-bit (AMD64 and Intel 64) device architecture.
```curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-darwin-amd64; mv kops bin/kops; chmod +x ./bin/kops ```

You must have an AWS account, generate IAM keys and configure them. The IAM user will need adequate permissions.
```pip install awscli```

CREATE CLUSTER
``` kops create cluster --cloud aws --name=kube.april.aws --state=s3://aks-aprilaws --zones=eu-west-1a --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=ccdpharmaedu.com  ```

That’s it. This command is used for creating the configuration of the cluster. To launch the cluster you can use the command:

``` kops update cluster kube.april.aws --yes --state=s3://aks-aprilaws --yes ```