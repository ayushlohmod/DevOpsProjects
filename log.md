
# 90 Days Of DevOps

## Log

### Day 000: Sep 24, 2023 (Script)

**Today's Progress**:

Today created a Bash script to monitor disk usage on a system and raise a "CRITICAL" alert if any of the disk partitions have usage greater than or equal to the specified threshold, which is set to 90% (alert=90).

```
#!/bin/bash
alert=90
df -H | awk '{print $5 " " $1}' | while read output;
do
#echo "Disk Detail: $output"
 usage=$(echo $output | awk '{print $1}' | cut -d'%' -f1)
 file_sys=$(echo $output | awk '{print $2}i')
 #echo $usage
if [ $usage -ge $alert ]
 then
        echo "CRITICAL for $file_sys"
fi
done
    
```

### Day 001: Oct 1, 2023 (DockerFile)

**Today's Progress**:
Today created a docker files for ruby on rails which run and install rails bundler
and run locally this will do automation for installing and upadating rails
```
FROM ruby:3.2.1
WORKDIR /app
RUN gem install rails bundler
COPY Gemfile Gemfile.lock ./
RUN bundle install
COPY . .
EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
```

### Day 002: Oct 2, 2023 (kubernetes)

**Today's Progress**:
Today created a kubernetes manifest file which deploy rails apps inside container
and run on PORT 3000
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rails-app
spec:
  replicas: 2 
  selector:
    matchLabels:
      app: rails-app
  template:
    metadata:
      labels:
        app: rails-app
    spec:
      containers:
      - name: rails-app-container
        image: ayush-rail-app-container
        ports:
        - containerPort: 3000
```

### Day 003: Oct 2, 2023 (kubernetes)

**Today's Progress**:
Today created a YAML file to Configure ArgoCD to Sync with My GitHub Repository
in this file i specify the source repository the path within the repository where my Kubernetes manifests are stored and other deployment-related configurations.

steps
1. Install ArgoCD on my Kubernetes cluster
2. Created a private GitHub repository to store my application's Kubernetes manifests and ArgoCD configuration files.
3. Configure ArgoCD to sync with my private GitHub repository by creating an Application YAML file

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-rails-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/ayushlohmod/K8-argoCD-files.git
    path: kubernnetes
    targetRevision: HEAD
  destination:
    server: https://kubernetes.default.svc
    namespace: my-rails-namespace

```
