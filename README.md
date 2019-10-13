# Monitoring Kubernetes with Prometheus -

### Perquisites - Kubernetes Cluster

### Steps required to setup Prometheus Monitoring on Kubernetes - 

1. Create a Namespace -

       # kubectl create namespace monitoring
  
2.  We have to  assign cluster reader permission to "monitoring" namespace so that Prometheus can fetch the metrics from
   Kubernetes API’s. 
   
        # kubectl create -f clusterRole.yaml

4. Create a Config Map -
     It contains all the configuration to dynamically discover pods and services running in the Kubernetes cluster
     
       # kubectl create -f config-map.yaml

5. Create a Prometheus Deployment - 
    We are also mounting the Prometheus config map as a file inside /etc/prometheus
    
       # kubectl create  -f prometheus-deployment.yaml 

6. Exposing Prometheus as a Service - 
   
       # kubectl create -f prometheus-service.yaml --namespace=monitoring

7. Connecting To Prometheus Dashboard - 
    a) Now go to URL which was generated from above step to access Prometheus Dashboard       
    b) Now if we browse to status --> Targets, we will see all the Kubernetes endpoints connected to Prometheus automatically using service discovery. Because of this we will get all Kubernetes container and Node metrics in Prometheus.
