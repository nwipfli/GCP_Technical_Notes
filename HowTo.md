- [Management Tools](#management-tools)
  - [Cloud Shell](#cloud-shell)
  - [Cloud Deployment Manager](#cloud-deployment-manager)
    - [Create](#create)
    - [Delete](#delete)
    - [Update](#update)
    - [List](#list)
- [Projects](#projects)
  - [Project](#project)
    - [List](#list-1)
    - [Change](#change)
    - [Set](#set)
  - [API](#api)
    - [Compute](#compute)
- [Accounts](#accounts)
  - [List](#list-2)
  - [Set](#set-1)
- [IAM](#iam)
  - [Projects](#projects-1)
  - [Roles](#roles)
  - [Service accounts](#service-accounts)
- [Compute](#compute-1)
  - [Compute Engine](#compute-engine)
    - [Instances](#instances)
      - [Lifecycle](#lifecycle)
        - [Create](#create-1)
        - [Delete](#delete-1)
        - [List](#list-3)
        - [Restart](#restart)
      - [Tags](#tags)
      - [Miscellaneous](#miscellaneous)
        - [RDP](#rdp)
        - [SSH](#ssh)
        - [Zones](#zones)
        - [OS specific commands](#os-specific-commands)
          - [Linux](#linux)
    - [Metadata](#metadata)
    - [Persistent disks](#persistent-disks)
      - [Create](#create-2)
  - [App Engine](#app-engine)
    - [Deployment](#deployment)
    - [Miscellaneous](#miscellaneous-1)
- [Hybrid and Multi-cloud](#hybrid-and-multi-cloud)
  - [Anthos](#anthos)
    - [Register](#register)
- [Storage](#storage)
  - [Cloud Storage](#cloud-storage)
    - [Create](#create-3)
    - [Copy](#copy)
    - [Versioning](#versioning)
- [Containers](#containers)
  - [Container Registry](#container-registry)
    - [Build](#build)
  - [Google Kubernetes Engine (GKE)](#google-kubernetes-engine-gke)
    - [General](#general)
      - [Operations](#operations)
      - [Miscellaneous](#miscellaneous-2)
    - [Cluster](#cluster)
      - [Create](#create-4)
      - [List](#list-4)
      - [Delete](#delete-2)
      - [Credentials](#credentials)
    - [Node pools](#node-pools)
    - [Security](#security)
      - [Network policy](#network-policy)
      - [PodSecurityPolicy](#podsecuritypolicy)
    - [Monitoring](#monitoring)
- [Networking](#networking)
  - [Virtual Private Cloud (VPC)](#virtual-private-cloud-vpc)
    - [Network](#network)
    - [Subnet](#subnet)
      - [Create](#create-5)
      - [List](#list-5)
      - [Increase](#increase)
      - [Flow logs](#flow-logs)
    - [Firewall](#firewall)
      - [Create](#create-6)
      - [Update](#update-1)
      - [List](#list-6)
  - [Load Balancers](#load-balancers)
    - [Healthcheck](#healthcheck)
    - [Backend service](#backend-service)
- [Databases](#databases)
  - [Cloud SQL](#cloud-sql)
    - [Instance](#instance)
      - [Create](#create-7)
      - [Connect](#connect)

# Management Tools

## Cloud Shell

- How to view which region is used for your current Cloud Shell session ?
  
  `curl metadata.google.internal/computeMetadata/v1/instance/zone`

- [How to configure your Cloud Shell ?](https://cloud.google.com/shell/docs/configuring-cloud-shell#custom_environments)

- [How to create a Cloud Shell custom environment ?](https://cloud.google.com/shell/docs/configuring-cloud-shell#environment_customization)

- How to start your Cloud Shell in safe mode ?
  - You need to append ***cloudshellsafemode=true*** to the URL and reload the page

## Cloud Deployment Manager

### Create

- How to build a deployment from a template ?
  
  ```bash
  gcloud deployment-manager deployments create \
  [deployment name] \
  --config [yaml file for template]
  ```
  
  ```bash
  gcloud deployment-manager deployments create \
  [deployment name] \
  --config=config.yaml \
  --preview
  ```
  
  ```bash
  gcloud deployment-manager deployments create \
  [deployment name] \
  --config=config.yaml
  ```

### Delete

- How to delete a deployment ?
  
  ```bash
  gcloud deployment-manager deployments delete \
  [deployment name]
  ```

### Update

- How to update a deployment ?
  
  ```bash
  gcloud deployment-manager deployments update \
  [deployment name] \
  --config [yaml file for template]
  ```
  
  ```bash
  gcloud deployment-manager deployments update \
  [deployment name]
  ```

### List

- How to list all available resource types ?
  
  ```bash
  gcloud deployment-manager types list
  ```

- How to list the deployments deployed ?
  
  ```bash
  gcloud deployment-manager deployments list
  ```

# Projects

## Project

### List

- How to list your project ?
  
  ```bash
  gcloud config list project
  ```

- How to get the project ID ?
  
  ```bash
  gcloud config get-value project -q
  ```

- How to list the configuration ?
  
  ```bash
  gcloud config list
  ```

- How to list all the properties ?
  
  ```bash
  gcloud config list --all
  ```

- How to list the details for a project ?
  
  ```bash
  gcloud compute project-info describe \
  --project <project_name>
  ```

### Change

- How to change to a different project ?
  
  ```bash
  gcloud config set project [PROJECT_ID]
  ```

### Set

- How to set the default zone ?
  
  ```bash
  gcloud config set compute/zone <zone>
  ```

- How to set the default region ?
  
  ```bash
  gcloud config set compute/region <region>
  ```

## API

### Compute

- How to enable the APIs ?
  
  ```bash
  gcloud services enable \
  container.googleapis.com \
  cloudbuild.googleapis.com \
  sourcerepo.googleapis.com \
  containeranalysis.googleapis.com
  ```

# Accounts

## List

- How to list your active account ?
  
  ```bash
  gcloud auth list
  ```

## Set

- How to set a different active account ?
  
  ```bash
  gcloud config set account [ACCOUNT]
  ```

# IAM

## Projects

- How to list all the roles assigned to users ?
  
  ```bash
  gcloud projects get-iam-policy [project name]
  ```

## Roles

- How to create a IAM role ?
  
  ```bash
  gcloud iam roles create \
  [role name] \
  --project [project name] \
  --file=[role-definition.yaml]
  ```

- How to disable a role ?
  
  ```bash
  gcloud iam roles update \
  [role name] \
  --project [project id] \
  --stage disabled
  ```

## Service accounts

- How to create a service account ?
  
  ```bash
  gcloud iam service-accounts create \
  [account_name] \
  --display-name "My Qwiklab Service Account"
  ```

- How to bind a role to a service account ?
  
  ```bash
  gcloud projects add-iam-policy-binding \
  [project id] \
  --member serviceAccount:qwiklab@projectid.iam.gserviceaccount.com \
  --role roles/owner
  ```

# Compute

## Compute Engine

### Instances

#### Lifecycle

##### Create

- How to create an instance ?
  
  ```bash
  gcloud compute instances create \
  [instance_name] \
  --machine-type [instance type] \
  --zone [zone] \
  --subnet=[subnet name]
  ```
  
  ```bash
  gcloud compute instances create \
  [instance_name] \
  --zone=us-central1-c \
  --machine-type=f1-micro \
  --subnet=privatesubnet-us
  ```
  
  ```bash
  gcloud compute instances create \
  [instance_name] \
  --machine-type=n1-standard-1 \
  --image-project=debian-cloud \
  --image=debian-9-stretch-v20190213 \
  --subnet=privatesubnet-us
  ```

##### Delete

- How to delete terminated instances ?
  
  ```bash
  #!/bin/bash
  for instance in  $(gcloud compute instances list --filter="status=terminated" --format="value(name)" --quiet)
  do
    zone=$(gcloud compute instances list --filter="name=$instance" --format="value(zone)" --quiet)

	status=$(gcloud compute instances describe $instance --zone=$zone --format="value(status)" --quiet)

	created_on=$(gcloud compute instances describe $instance \
	--zone=$zone \
	--format="value(creationTimestamp.date('%Y-%m-%d'))" \
	--quiet)

	echo "Instance name: $instance"

	echo "Created on $created_on"

	gcloud compute instances delete $instance --zone=$zone --quiet
  done
  ```

##### List

- How to list the instances ?
  - Sorted by zone
  
    ```bash
  	gcloud compute instances list --sort-by=ZONE
	```

  - Only terminated instances
  
    ```bash
	gcloud compute instances list --filter="status=terminated"
	```
  
    - Show only the zones

		```bash
		gcloud compute instances list \
		--filter="status=terminated" \
		--format=”value(zone)”
		```

##### Restart

- How to restart instances ?

  - When free memory is below 5000

	```bash
	#!/bin/bash
	ZONE=us-central1-a
	MIN_MEMORY=5000
	for instance in $(gcloud compute instances list --format="value(name)"
					--filter="zone:$ZONE status:running" --quiet)
	do
	free_memory=$(gcloud compute ssh $instance --zone=$ZONE --command="free -m |
					awk '/^Mem:/{print \$4}'" --quiet)
	if (( $free_memory < $MIN_MEMORY ))
	then
		echo "Restarting instance : $instance"
		gcloud compute instances stop $instance --zone=$ZONE --quiet
		gcloud compute instances start $instance --zone=$ZONE --quiet
	fi
	done
	```

#### Tags

- How to add a target tag to a VM ?
  
  ```bash
  gcloud compute instances add-tags \
  [instance_name] \
  --zone europe-west1-b \
  --tags lab-ssh
  ```

#### Miscellaneous

##### RDP

- How to check whether the instance is ready for an RDP connection ?
  
  ```bash
  gcloud compute instances get-serial-port-output
  ```

##### SSH

- How to ssh to a Linux instance ?
  
  ```bash
  gcloud compute ssh \
  [instance_name] \
  --zone [zone]
  ```

- How to ssh to a Linux instance using the IAP connection ?
  
  ```bash
  gcloud compute ssh \
  [instance_name] \
  --zone [zone] \
  --tunnel-through-iap
  ```

##### Zones

- How to list all the zones ?
  
  ```bash
  gcloud compute zones list
  ```

- How to set the default zone ?
  
  ```bash
  gcloud config set compute/zone [zone]
  ```

##### OS specific commands

###### Linux

- How to see the details about the RAM installed on your Linux VM ?
  
  ```bash
  sudo dmidecode -t 17
  ```

- How to see the details about the CPU installed on your Linux VM ?
  
  ```bash
  lscpu
  ```

### Metadata

- How to fetch metadata ?
  
  ```bash
  curl metadata.google.internal/computeMetadata/v1/
  ```

- How to find the instance external IP by querying the metadata ?
  
  ```bash
  curl -H "Metadata-Flavor: Google" http://169.254.169.254/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip && echo
  ```

### Persistent disks

#### Create

- How to create a persistent disk ?
  
  ```bash
  gcloud compute disks create \
  --size=100GB \
  --zone=us-central1-a \
  demo-disk
  ```

## App Engine

### Deployment

- How to deploy your app ?
  
  ```bash
  gcloud app deploy
  ```
  
  ```bash
  gcloud app deploy --version=one --quiet
  ```

- How to deploy a new version without promoting ?
  
  ```bash
  gcloud app deploy \
  --version=two \
  --no-promote \
  --quiet
  ```

### Miscellaneous 

- How to browse your app ?
  
  ```bash
  gcloud app browse
  ```

- How to initialize your App Enginee App with your project ?
  
  ```bash
  gcloud app create --project=[project ID]
  ```

# Hybrid and Multi-cloud

## Anthos

### Register

- How to register a remote GKE cluster ?
  
  ```bash
  gcloud container hub memberships register [REMOTE_CLUSTER_NAME] \
  --context=[REMOTE_CLUSTER_NAME] \
  --service-account-key-file=[GKE_SA_CREDS] \
  --project=[PROJECT]
  ```

# Storage

## Cloud Storage

### Create

- How to create a bucket ?
  
  ```bash
  gsutil mb gs://[BUCKET_NAME]
  ```

### Copy

- How to copy a file into a bucket ?
  
  ```bash
  gsutil cp [MY_FILE] gs://[BUCKET_NAME]
  ```

### Versioning

- How to enable versioning ?
  
  ```bash
  gsutil versioning set on [gs://whizlabs-bucket]
  ```

# Containers

## Container Registry

### Build

- How to build an image ?
  
  ```bash
  gcloud builds submit \
  --tag=gcr.io/$PROJECT_ID/gcp-gke-monitor-test .
  ```

  ```bash
  docker build \
  -t gcr.io/$PROJECT_ID/gcp-gke-monitor-test .
  ```

## Google Kubernetes Engine (GKE)

### General

#### Operations

- How to list the ongoing operations ?
  
  ```bash
  gcloud container operations list
  ```

- How to monitor an ongoing operation ?
  
  ```bash
  gcloud container operations wait \
  [operation_id] \
  --zone=[zone]
  ```

#### Miscellaneous

- How to configure kubectl tab completion ?
  
  ```bash
  source <(kubectl completion bash)
  ```

### Cluster

#### Create

- How to create a kubenertes cluster ?
  
  ```bash
  gcloud container clusters create \
  [cluster_name] \
  --zone [zone] \
  --num-nodes [number of node]
  ```
  
  ```bash
  gcloud container clusters create \
  [cluster_name] \
  --zone $MY_ZONE \
  --num-nodes 2
  ```

  - With autoscaling enabled

	```bash
	gcloud container clusters create \
	[cluster_name] \
	--zone [zone] \
	--num-nodes [number of node] \
	--enable-autoscaling \
	--min-nodes [min_number_of_node] \
	--max-nodes [max_number_of_node]
	```

  - With network policy enabled
  	
	```bash
	gcloud container clusters create \
	[cluster_name] \
	--enable-network-policy
	```

#### List

- How to get the details of a cluster ?
  
  ```bash
  gcloud container clusters describe \
  [cluster_name] \
  --region [region]
  ```

#### Delete

- How to delete a kubernetes cluster ?
  
  ```bash
  gcloud container clusters delete \
  [CLUSTER-NAME]
  ```

#### Credentials

- How to get the credentials for the GKE cluster ?
  
  ```bash
  gcloud container clusters \
  get-credentials [cluster_name] \
  --zone [zone_name]
  ```

- How to initiate the rotation of the IP address and credentials ?
  
  ```bash
  gcloud container clusters update \
  [cluster_name] \
  --zone [zone] \
  --start-credential-rotation
  ```

- How to complete the credential and IP rotation ?
  
  ```bash
  gcloud container clusters update \
  [cluster_name] \
  --zone [zone] \
  --complete-credential-rotation
  ```

### Node pools

- How to add a node pool with autoscaling enabled ?
  
  ```bash
  gcloud container node-pools create \
  [pool_name] \
  --cluster [cluster_name] \
  --enable-autoscaling \
  --min-nodes [min_number_of_node] \
  --max-nodes [max_number_of_node]
  ```

- How to enable autoscaling for an existing node pool ?
  
  ```bash
  gcloud container clusters update \
  [cluster_name] \
  --enable-autoscaling \
  --min-nodes [min_number_of_node] \
  --max-nodes [max_number_of_node] \
  --node-pool [pool_name]
  ```

- How to disable autoscaling for an existing node pool ?
  
  ```bash
  gcloud container clusters update \
  [cluster_name] \
  --no-enable-autoscaling \
  --node-pool [pool_name] \
  --project [project_ID]
  ```

### Security

#### Network policy

- How to enable network policy for an existing cluster ?
  
  ```bash
  gcloud container clusters update \
  [cluster_name] \
  --update-addons-NetworkPolicy=ENABLED
  ```
  
  ```bash
  gcloud container clusters update \
  [cluster_name] \
  --enable-network-policy
  ```

- How to disable a network policy ?
  
  ```bash
  gcloud container clusters create \
  [cluster_name] \
  --no-enable-network-policy
  ```

#### PodSecurityPolicy

- How to enable a PodSecurity Policy ?
  
  ```bash
  gcloud container clusters update \
  [cluster_name] \
  --enable-pod-security-policy
  ```

- How to disable a PodSecurity Policy ?
  
  ```bash
  gcloud container clusters update \
  [CLUSTER_NAME] \
  --no-enable-pod-security-policy
  ```

### Monitoring

- How to verify that Kubernetes Engine Monitoring is enabled ?
  
  ```bash
  kubectl get daemonsets.apps \
  -n kube-system prometheus-to-sd
  ```

# Networking

## Virtual Private Cloud (VPC)

### Network

- How to list the available VPC networks ?
  
  ```bash
  gcloud compute networks list
  ```

- How to create a custom VPC network ?
  
  ```bash
  gcloud compute networks create managementnet \
  --project=[project ID] \
  --subnet-mode=custom \
  --bgp-routing-mode=regional
  ```

### Subnet

#### Create

- How to create a subnet ?
  
  ```bash
  gcloud compute networks subnets create \
  [subnet name] \
  --project=[project ID] \
  --range=[subnet CIDR] \
  --network=[network name] \
  --region=[region]
  ```

#### List

- How to list the available subnets (sorted by VPC network) ?
  
  ```bash
  gcloud compute networks subnets list --sort-by=NETWORK
  ```

- How to list the details of a subnet ?
  
  ```bash
  gcloud compute networks subnets describe \
  [subnet_name] \
  --region [region]
  ```

#### Increase

- How to increase a subnet range ?
  
  ```bash
  gcloud compute networks subnets expand-ip-range \
  [subnet_name] \
  --prefix-length=PREFIX_LENGTH
  ```

#### Flow logs

- How to enable flow logs for a specific subnet ?
  
  ```bash
  gcloud compute networks subnets update \
  [subnet_name] \
  --region us-central1 \
  --enable-flow-logs
  ```

- How to disable flow logs for a specific subnet ?
  
  ```bash
  gcloud compute networks subnets update \
  [subnet_name] \
  --region europe-west1 \
  --no-enable-flow-logs
  ```

### Firewall

#### Create

- How to create firewall rules ?
  
  ```bash
  gcloud compute firewall-rules create \
  [rule_name] \
  --direction=[] \
  --priority=[] \
  --network=m[network name] \
  --action=[ALLOW | DENY] \
  --rules=[] \
  --source-ranges=[IP]
  ```
  
  ```bash
  gcloud compute firewall-rules create managementnet-allow-icmp-ssh-rdp \
  --direction=INGRESS \
  --priority=1000 \
  --network=managementnet \
  --action=ALLOW \
  --rules=tcp:22,tcp:3389,icmp \
  --source-ranges=0.0.0.0/0
  ```
  
  ```bash
  gcloud compute firewall-rules create \
  [rule_name] \
  --network [network name] \
  --allow tcp:22,tcp:3389,icmp
  ```

#### Update

- How to update a firewall rule ?
  
  ```bash
  gcloud compute firewall-rules update \
  [rule_name] \
  --priority 2000
  ```

#### List

- How to list the firewall rules ?
  
  ```bash
  gcloud compute firewall-rules list \
  --filter="network:mynetwork"
  ```
  
  ```bash
  gcloud compute firewall-rules list \
  --filter network=network3
  ```
  
  ```bash
  gcloud compute firewall-rules list \
  --sort-by=NETWORK
  ```

  - Sorted by VPC network
  
	```bash
	gcloud compute firewall-rules list --sort-by=NETWORK
	```

## Load Balancers

### Healthcheck

- How to create a healthcheck ?
  
  ```bash
  gcloud compute http-health-checks create http-basic-check
  ```

### Backend service

- How to create a backend service ?
  
  ```bash
  gcloud compute backend-services create \
  [back-end_service_name] \
  --protocol HTTP \
  --http-health-checks http-basic-check \
  --global
  ```

- How to add an instance group to a backend service ?
  
  ```bash
  gcloud compute backend-services add-backend \
  [back-end_service_name] \
  --instance-group nginx-group \
  --instance-group-zone us-central1-a \
  --global
  ```

# Databases

## Cloud SQL

### Instance

#### Create

- How to create an instance ?
  
  ```bash
  gcloud sql instances create \
  [instance_name] \
  --tier=db-n1-standard-2 \
  --region=us-central1
  ```

#### Connect

- How to connect to an instance ?
  
  ```bash
  gcloud sql connect \
  [instance_name]
  ```