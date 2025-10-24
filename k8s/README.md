# **XOps Microchallenge #8 – ConfigMaps vs Secrets**



### This challenge has been designed for understanding how application configurations that are non-sensitive such as environment settings, feature flags and application properties are handled.





#### **Objective**:



##### Show how to manage non-sensitive configs (like app.properties, feature flags, or environment variables) using Kubernetes ConfigMaps, and compare with Secrets.





#### Files:



##### \- configmap.yaml - ConfigMap named app-config with non-sensitive app configuration.

##### \- config-env-pod.yaml - Pod that loads `app-config` via envFrom (environment variables).

##### \- config-vol-pod.yaml - Pod that mounts `app-config` as files under /etc/config.

##### \- secret.yaml - Demo Secret db-creds (fake credentials for comparison).

##### \- secret-pod.yaml - Pod that injects Secret values as environment variables.



#### Step-by-step instructions:



###### **1. Apply the ConfigMap and Secret**



###### kubectl apply -f configmap.yaml

###### kubectl apply -f secret.yaml

###### 

###### **2.Verify the ConfigMap and Secret exist**



###### kubectl get configmap

###### kubectl describe configmap app-config

###### 

###### kubectl get secret

###### kubectl describe secret db-creds

###### 

#### 3.Create the pods

###### 

###### kubectl apply -f config-env-pod.yaml

###### kubectl apply -f config-vol-pod.yaml    

###### kubectl apply -f secret-pod.yaml

###### 

#### 4.Wait for pods to enter Running (sleep-ing pod will be ready fast)

##### 

##### kubectl get pods -l app=config-demo -w

##### \# or

##### kubectl get pods



#### 5.Verify ConfigMap injected as environment variables



###### kubectl exec -it config-env-pod -- env | grep -E "APP\_MODE|FEATURE\_X\_ENABLED"





#### 6.Verify ConfigMap mounted as files (optional)



###### kubectl exec -it config-vol-pod -- ls -l /etc/config

###### kubectl exec -it config-vol-pod -- cat /etc/config/APP\_MODE

###### kubectl exec -it config-vol-pod -- cat /etc/config/FEATURE\_X\_ENABLED





