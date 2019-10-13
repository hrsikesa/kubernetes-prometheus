# Monitoring Kubernetes with Prometheus -

### Perquisites - Kubernetes Cluster

### Steps required to setup Prometheus Monitoring on Kubernetes - 

1. Create a Namespace -

       # kubectl create namespace monitoring
  
2.  We have to  assign cluster reader permission to "monitoring" namespace so that Prometheus can fetch the metrics from
   Kubernetes API’s.   [clusterRole.yaml](https://github.com/hrsikesa/kubernetes-prometheus/blob/master/clusterRole.yaml)

   
        # kubectl create -f clusterRole.yaml
4. Create a Config Map -
     It contains all the configuration to dynamically discover pods and services running in the Kubernetes cluster. [config-map.yaml](https://github.com/hrsikesa/kubernetes-prometheus/blob/master/config-map.yaml)
     
       # kubectl create -f config-map.yaml

5. Create a Prometheus Deployment - 
    We are also mounting the Prometheus config map as a file inside /etc/prometheus. [prometheus-deployment.yaml](https://github.com/hrsikesa/kubernetes-prometheus/blob/master/prometheus-deployment.yaml)
    
       # kubectl create  -f prometheus-deployment.yaml 

6. Exposing Prometheus as a Service - [prometheus-service.yaml](https://github.com/hrsikesa/kubernetes-prometheus/blob/master/prometheus-service.yaml)
   
       # kubectl create -f prometheus-service.yaml --namespace=monitoring

7. Connecting To Prometheus Dashboard - 
    a) Now go to URL which was generated from above step to access Prometheus Dashboard       
    b) Now if we browse to status --> Targets, we will see all the Kubernetes endpoints connected to Prometheus automatically using service discovery. Because of this we will get all Kubernetes container and Node metrics in Prometheus.
