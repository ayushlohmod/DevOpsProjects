
# 90 Days Of DevOps

## Log

### Day 000: Sep 24, 2023 (Script)

**Today's Progress**:

Today created a Bash script to monitor disk usage on a system and raise a "CRITICAL" alert if any of the disk partitions have usage greater than or equal to the specified threshold, which is set to 90% (alert=90).

```bash
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
```dockerfile
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
```yaml
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

```yaml
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
### Day 004: Oct 10, 2023 (Docker)

**Today's Progress**:
Installed Docker Compose learn to use it also created a Yaml file to set up the environment, configure the services and links between different containers, and also to use environment variables in the docker-compose.yml file.

The File looks like this
```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    networks:
      - mynetwork
  db:
    image: mysql:latest
    environment:
      - MYSQL_ROOT_PASSWORD=my-secret-pw
    networks:
      - mynetwork
networks:
  mynetwork:


```

### Day 004: Oct 11, 2023 (Docker)

**Today's Progress**:
Today build a project 
1 where i Fork the github repository 
2 Create a connection to my Jenkins job and my GitHub Repository via GitHub Integration.
3 In the Execute shell I run the application using Docker compose
4 the project run on port 8000

**Link to work:**

- https://github.com/ayushlohmod/ToDo-cicd

### Day 004: Dec 06, 2023 (Aws)
Since i was working with aws quite alot i know mostly services 
Learn All about aws completed task 

### Day 004: Dec 07, 2023 (Ci/CD)
**Today's Progress**:

Learn About CodeBuild
Read about Buildspec file for Codebuild.
created a simple index.html file in CodeCommit Repository
build the index.html using nginx server

