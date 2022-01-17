# FastAPI websvc-env
Python FastAPI webapi for testing
You need curl, docker, docker-compose, helm, and python/pip + conda for local dev

## -- Get repository for read-write access
````
ssh-agent bash -c 'ssh-add ~/.ssh/id_rsa; git clone git@github.com:eossf/websvc-env.git'
git config --global user.email "stephane.metairie@gmail.com"
````

## -- Run locally in VSCode
````
conda env create
conda activate WEBSVCENV
uvicorn main:app
````

## -- Build Image
````
cd ~/websvc-env
docker build . -t websvc-env:0.0.1
docker-compose build --force-rm --progress plain
````

## -- Helm deploy package

### create a namespace, add context
````
kubectl create namespace int
kubectl create namespace qual
kubectl create namespace preprod
kubectl create namespace prod
````

## -- Deployment

### install websvc-env package INTEGRATION
````
cd ~/websvc-env
helm install -f ../deploy/int.yaml websvc-env ./websvc-env
````


## -- test an environment

For INT NodePort 32000 
````
helm install -f ../deploy/INT/int.yaml websvc-env ./websvc-env
curl http://NODE01:32000/info 
#default : curl http://45.76.46.182:32000/info 

````