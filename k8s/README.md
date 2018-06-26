# k8s-workshop

K8s Workshop for my awesome ISD TEAM

<p align="center">
<img src="https://raw.githubusercontent.com/gaelleiadvize/k8s-workshop/master/img/isd.png" width="150">
<img src="https://raw.githubusercontent.com/gaelleiadvize/k8s-workshop/master/img/k8s.png" width="150">
</p>

## Setup

Before you can run or deploy the sample, you need to do the following:

1.  Install homebrew:

      Run this in your terminal 
    
        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    [See more doc here][homebrew]
    
2.  Install Yarn globaly

    Run this in your terminal 
        
            brew install yarn


3.  Install Docker4mac (Edge):

    [Get last release here][docker4Mac]


## Install Environment : 


####  ** Docker For Mac (Edge) **

[Get last release here][docker4Mac]


#### ** GCLOUD SDK **


1. Enter the following at a command prompt:

        curl https://sdk.cloud.google.com | bash
        
2. Restart your shell:

        exec -l $SHELL OR source ~/.zshrc
     
3. Run `gcloud init` to initialize the `gcloud` environment:

        gcloud init
            
   Continue authentication ...  
            
 
#### ** Kubectl SDK **

Prerequis - Homebrew : https://brew.sh/index_fr


    gcloud components install kubectl           
            

## Cluster authentication



- List clusters : 


    gcloud container clusters list


- Get credential 
    
    
    gcloud container clusters get-credentials {CLUSTER_NAME} --project {PROJECT_ID} --zone europe-west1


- View namespaces :


    kubectl get namespaces


- View current context

    
    kubectl config current-context



- Switch to your namespace : 


    kubectl config set-context $(kubectl config current-context) --namespace={NAMESPACE}
    


## Deploy your first APP :


### Run App locally

        
#### - Clone the repository: 

 https://github.com/gaelleiadvize/k8s-workshop
 

    git clone git@github.com:gaelleiadvize/k8s-workshop.git
    
    cd k8s-workshop/k8s/hello-world
    
    yarn install
    yarn start
    
    
  See  <a href="http://localhost:8080" target="blank">http://localhost:8080</a>

<p align="center">
<img src="https://i.giphy.com/l3q2SH4Cmhh8F40jS.gif">
</p>


<p align="center">It works ! Go to k8s now 😛 </p>




#### -  Build / Push docker images


    cd k8s-workshop/k8s/hello-world
    
   => View DockerFile & explain
    
    # build docker image : 
    docker build -t eu.gcr.io/dev-production/hello-world-{gacas}:v1 .
    
    # push docker image : 
    docker push eu.gcr.io/dev-production/hello-world-{gacas}:v1




#### - Deployment :

    cd k8s-workshop/k8s/deploy
    
   Explain what is a deployment ??????
    
   edit deployment.yaml file with your editor
   set your namespace : ex mynamespace
   
       apiVersion: extensions/v1beta1
       kind: Deployment
       metadata:
         name: hello-world
         namespace: mynamespace
       spec:
         replicas: 1
         strategy:
        [...]
  
  And Apply :  
  
  
    # Apply deployment 
    kubectl apply -f deployment.yaml
    
    
    
    # list deployments : 
    kubectl get deployment
    NAME          DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
    hello-world   1         1         1            1           1h   
    
   
    

#### - Expose app with service (service.yaml) :
    
    cd k8s-workshop/k8s/deploy
    
   * Edit service.yaml & set your namespace : ex mynamespace
    
    apiVersion: v1
    kind: Service
    metadata:
      name: hello-world
      namespace: mynamespace
    spec:
      ports:
      - port: 80
        targetPort: 8080
        protocol: TCP
      type: NodePort
      selector:
        app: hello-world
    
   * Apply : 
   
    # Apply service 
    kubectl apply -f service.yaml

    # list service : 
    kubectl get service
    NAME          TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
    hello-world   NodePort       10.7.252.74   <none>          80:30986/TCP   1h


#### -  Expose app to the world :


    cd k8s-workshop/k8s/deploy
    
   * Edit service.yaml
    
    change 
     type: NodePort
     to 
     type: LoadBalancer
    
    # Apply service 
    kubectl apply -f service.yaml


    # list service : 
    kubectl get service
    NAME          TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
    hello-world   LoadBalancer   10.7.252.74   35.195.106.40   80:30986/TCP   1h


Go to http://{EXTERNAL-IP} 

 
<p align="center">
that’s all !
</p>
<p align="center">
<img src="https://i.giphy.com/3o6gEaYbewKku0GwPS.gif">
</p>   
 
    
    
    
    
    
    
    
    
[homebrew]: https://brew.sh/index_fr
[docker4Mac]: https://docs.docker.com/docker-for-mac/edge-release-notes/