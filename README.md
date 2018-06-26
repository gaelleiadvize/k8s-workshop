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


## Run App locally

1.  Go to root app directory & run :

        yarn install
2.  run 
        
        npm run start-dev
    or 
        npm run start   
        
<p align="center">
<img src="https://i.giphy.com/l3q2SH4Cmhh8F40jS.gif">
</p>


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
    
#Deploy your first APP :

          
[homebrew]: https://brew.sh/index_fr
[docker4Mac]: https://docs.docker.com/docker-for-mac/edge-release-notes/