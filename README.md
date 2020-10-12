# Provision an EKS Cluster

```
$ aws configure
AWS Access Key ID [None]: YOUR_AWS_ACCESS_KEY_ID
AWS Secret Access Key [None]: YOUR_AWS_SECRET_ACCESS_KEY
Default region name [None]: YOUR_AWS_REGION
Default output format [None]: json
```

# Initialize Terraform workspace

```
terraform init
```

# View the plan before applying changes

```
terraform plan
```

# Deploy EKS cluster and Apply changes to the infrastructure

```
terraform apply
```

# Connect to EKS cluster

```
aws eks --region eu-west-2 update-kubeconfig --name [cluster name]
```


# Apply Kubernetes secrets

```
kubectl apply -f mysqlSecrets.yml
```

# Create deployment in Kubernetes using kubectl apply command

```
kubectl apply -f mysqlDeployment.yml
```

# Create Service resource using kubectl apply command

```
kubectl apply -f mysqlServices.yml
```

# Build Docker image 

```
docker build -t activemq
```

# Push Docker image to docker hub

```
docker push activemq
```

# Create Secret

```
kubectl create secret generic creds --from-file=jetty-realm.properties -n active-mq
```

# Deploy Activmq service

```
kubectl create -f service.yaml
```


# Deploy Redis on Kubernetes


## Namespace

```
kubectl create ns redis
```


```
kubectl apply -n redis -f ./redis/redis-configmap.yaml
kubectl apply -n redis -f ./redis/redis-statefulset.yaml

kubectl  redis get pods
kubectl  redis get pv

kubectl -n redis logs redis-0
kubectl -n redis logs redis-1
kubectl -n redis logs redis-2
```

## Test replication status

```
kubectl -n redis exec -it redis-0 sh
redis-cli 
auth a-very-complex-password-here
info replication
```

## Deployment: Redis Sentinel (3 instances)

```
kubectl apply -n redis -f ./sentinel/sentinel-statefulset.yaml

kubectl -n redis get pods
kubectl -n redis get pv
kubectl -n redis logs sentinel-0
```
