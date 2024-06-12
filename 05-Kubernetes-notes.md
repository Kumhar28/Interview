
# Course Objectives

# Kubernetes Bacics
## Cluster Architecture

  
![Kubernetes Architecture 1](images/k8s-arch1.PNG)

K8s Reference Docs:
- https://kubernetes.io/docs/concepts/architecture/

[this link](https://kubernetes.io/docs/reference/tools/map-crictl-dockercli/#retrieve-debugging-information).

### ETCD
## What is a ETCD?
- ETCD is a distributed reliable key-value store that is simple, secure & Fast.
- The ETCD Datastore stores information regarding the cluster such as **`Nodes`**, **`PODS`**, **`Configs`**, **`Secrets`**, **`Accounts`**, **`Roles`**, **`Bindings`** and **`Others`**.
- Every information you see when you run the **`kubectl get`** command is from the **`ETCD Server`**.

### Kube API Server

#### Kube-apiserver is the primary component in kubernetes.
- Kube-apiserver is responsible for **`authenticating`**, **`validating`** requests, **`retrieving`** and **`Updating`** data in ETCD key-value store. 
- In fact kube-apiserver is the only component that interacts directly to the etcd datastore. 
- The other components such as kube-scheduler, kube-controller-manager and kubelet uses the API-Server to update in the cluster in their respective areas.
  
  ![post](images/post.PNG)
  
### Kube Controller Manager

#### Kube Controller Manager manages various controllers in kubernetes.
- In kubernetes terms, a controller is a process that continuously monitors the state of the components within the system and works towards bringing the whole system to the desired functioning state.

#### Node Controller
   - Responsible for monitoring the state of the Nodes and taking necessary actions to keep the application running. 
  
   
#### Replication Controller
   - It is responsible for monitoring the status of replicasets and ensuring that the desired number of pods are available at all time within the set.
   
   
#### Other Controllers
   - There are many more such controllers available within kubernetes
    

### Kube Scheduler

#### kube-scheduler is responsible for scheduling pods on nodes.  
- The kube-scheduler is only responsible for deciding which pod goes on which node. 
- It doesn't actually place the pod on the nodes, that's the job of the **`kubelet`**.
 

### Kubelet

#### Kubelet is the sole point of contact for the kubernetes cluster
- The **`kubelet`** will create the pods on the nodes, the scheduler only decides which pods goes where.
  
### Kube Proxy
- Within Kubernetes Cluster, every pod can reach every other pod, this is accomplish by deploying a pod networking cluster to the cluster. 
- Kube-Proxy is a process that runs on each node in the kubernetes cluster.

### Container Runtime:
- Software responsible for running containers (e.g., Docker, containerd).
- Pulls container images, creates containers, and manages their lifecycle.

## High-Level Example Workflow:
1. A user deploys a Kubernetes manifest specifying desired pod configurations.
2. The manifest is submitted to the API server.
3. The API server stores the configuration in etcd.
4. The Controller Manager detects the desired state and instructs the Kubelet on
worker nodes to start or stop containers.
5. Kubelet communicates with the container runtime to execute the desired
state.
6. Kube Proxy manages network rules, enabling communication between pods.


### Pods
- The smallest deployable unit in Kubernetes.
- A pod represents a single instance of a running process in a cluster and
encapsulates one or more containers

### Multi-Container PODs
- A single pod can have multiple containers except for the fact that they are usually not multiple containers of the **`same kind`**.
  
### ReplicaSets
#### Controllers are brain behind kubernetes
## Difference between ReplicaSet and Replication Controller
- **`Replication Controller`** is the older technology that is being replaced by a **`ReplicaSet`**.
- **`ReplicaSet`** is the new way to setup replication.

### Creating a Replication Controller

### Replication Controller Definition File
  
   ![rc2](images/rc2.PNG)
  
```yaml
    apiVersion: v1
    kind: ReplicationController
    metadata:
      name: myapp-rc
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx
     replicas: 3
```
  - To Create the replication controller
    ```
    $ kubectl create -f rc-definition.yaml
    ```
  - To list all the replication controllers
    ```
    $ kubectl get replicationcontroller
    ```
  - To list pods that are launch by the replication controller
    ```
    $ kubectl get pods
    ```
    ![rc3](images/rc3.PNG)
    
### Creating a ReplicaSet
  
#### ReplicaSet Definition File

   ![rs](images/rs.PNG)

```
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
      name: myapp-replicaset
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        type: front-end
 ```
#### ReplicaSet requires a selector definition when compare to Replication Controller.
   
  - To Create the replicaset
    ```
    $ kubectl create -f replicaset-definition.yaml
    ```
  - To list all the replicaset
    ```
    $ kubectl get replicaset
    ```
  - To list pods that are launch by the replicaset
    ```
    $ kubectl get pods
    ```
  

### Deployments

- A Deployment in Kubernetes describes a desired state for a set of identical pods. 
- It allows you to declaratively manage applications, including their replicas, updates, and rollbacks.
  
#### How do we create deployment?

```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp-deployment
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        type: front-end
 ```
- Once the file is ready, create the deployment using deployment definition file
  ```
  $ kubectl create -f deployment-definition.yaml
  ```
- To see the created deployment
  ```
  $ kubectl get deployment
  ```
- The deployment automatically creates a **`ReplicaSet`**. To see the replicasets
  ```
  $ kubectl get replicaset
  ```
- The replicasets ultimately creates **`PODs`**. To see the PODs
  ```
  $ kubectl get pods
  ```
    
  ![deployment1](images/deployment1.PNG)
  
- To see the all objects at once
  ```
  $ kubectl get all
  ```
  ![deployment2](images/deployment2.PNG)
  

### Namespaces

So far in this course we have created **`Objects`** such as **`PODs`**, **`Deployments`** and **`Services`** in our cluster. Whatever we have been doing we have been doing in a **`NAMESPACE`**.
- This namespace is the **`default`** namespace in kubernetes. It is automatically created when kubernetes is setup initially.

## Kubernetes Services
- In Kubernetes, Services are used to expose applications running in a set of Pods as a network service. There are different types of Services, each with its own use case.
Here are some common Service types:
### ClusterIP:
- A ClusterIP Service exposes the Service on an internal IP address within the cluster.
- This type of Service is only reachable from within the cluster.
```yaml
apiVersion: v1
kind: Service
metadata:
 name: example-clusterip-service
spec:
 selector:
 app: example
 ports:
 - protocol: TCP
 port: 80
 targetPort: 8080
```
### NodePort:
- A NodePort Service exposes the Service on each Node's IP at a static port. It makes the Service accessible externally by connecting to any Node's IP on the specified NodePort.
```yaml
apiVersion: v1
kind: Service
metadata:
 name: example-nodeport-service
spec:
 selector:
 app: example
 ports:
 - protocol: TCP
 port: 80
 targetPort: 8080
 type: NodePort
```
### LoadBalancer:
- A LoadBalancer Service automatically provisions an external load balancer in cloud environments (e.g., AWS, GCP) and assigns a public IP to the Service. It is useful for exposing services to the internet.
```yaml
apiVersion: v1
kind: Service
metadata:
 name: example-loadbalancer-service
spec:
 selector:
 app: example
 ports:
 - protocol: TCP
 port: 80
 targetPort: 8080
 type: LoadBalancer
```
### ExternalName:
- An ExternalName Service maps a Service to a DNS name. It is used for accessing
external services by name.
```yaml
apiVersion: v1
kind: Service
metadata:
 name: example-externalname-service
spec:
 type: ExternalName
 externalName: example.com
```
### Headless Service:
- A Headless Service is used when you don't need load balancing or a single IP. 
- It provides DNS resolution for the set of Pods but doesn't allocate a cluster IP.
```yaml
apiVersion: v1
kind: Service
metadata:
 name: example-headless-service
spec:
 clusterIP: None
 selector:
 app: example
 ports:
 - protocol: TCP
 port: 80
 targetPort: 8080
```
### Ingress:
- While not a Service type per se, an Ingress is often used to expose HTTP and HTTPS routes to services within the cluster. 
- It provides more advanced routing capabilities compared to basic Services.
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
 name: example-ingress
spec:
 rules:
 - host: example.com
 http:
 paths:
 - path: /app
 pathType: Prefix
 backend:
 service:
 name: example-service
 port:
 number: 80
```
- Choose the Service type that best fits your application's requirements and the
desired level of exposure. 
- Always consider security implications when exposing services externally


## Annotations
- While labels and selectors are used to group objects, annotations are used to record other details for informative purpose.
```yaml
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
      name: simple-webapp
      labels:
        app: App1
        function: Front-end
      annotations:
         buildversion: 1.34
    spec:
     replicas: 3
     selector:
       matchLabels:
        app: App1
    template:
      metadata:
        labels:
          app: App1
          function: Front-end
      spec:
        containers:
        - name: simple-webapp
          image: simple-webapp   
```
![annotations](images/annotations.PNG)

## Taints and Tolerations
- Pod to node relationship and how you can restrict what pods are placed on what nodes.

#### Taints and Tolerations are used to set restrictions on what pods can be scheduled on a node. 
- Only pods which are tolerant to the particular taint on a node will get scheduled on that node.

![tandt](images/tandt.PNG)
  
### Taints
- Use **`kubectl taint nodes`** command to taint a node.

  Syntax
  ```
  $ kubectl taint nodes <node-name> key=value:taint-effect
  ```
 
  Example
  ```
  $ kubectl taint nodes node1 app=blue:NoSchedule
  ```
  
- The taint effect defines what would happen to the pods if they do not tolerate the taint.
- There are 3 taint effects
  - **`NoSchedule`**
  - **`PreferNoSchedule`**
  - **`NoExecute`**
  
![tn](images/tn.PNG)
  
### Tolerations
- Tolerations are added to pods by adding a **`tolerations`** section in pod definition.
```yaml
     apiVersion: v1
     kind: Pod
     metadata:
      name: myapp-pod
     spec:
      containers:
      - name: nginx-container
        image: nginx
      tolerations:
      - key: "app"
        operator: "Equal"
        value: "blue"
        effect: "NoSchedule"
```
    
  ![tp](images/tp.PNG)
    

#### Taints and Tolerations do not tell the pod to go to a particular node. Instead, they tell the node to only accept pods with certain tolerations.
- To see this taint, run the below command
  ```
  $ kubectl describe node kubemaster |grep Taint
  ```
 
 ![tntm](images/tntm.PNG)
  


## Node Selectors
#### We add new property called Node Selector to the spec section and specify the label.
- The scheduler uses these labels to match and identify the right node to place the pods on.

```yaml
  apiVersion: v1
  kind: Pod
  metadata:
   name: myapp-pod
  spec:
   containers:
   - name: data-processor
     image: data-processor
   nodeSelector:
    size: Large
```
![nsel](images/nsel.PNG)
  
- To label nodes

  Syntax
  ```
  $ kubectl label nodes <node-name> <label-key>=<label-value>
  ```
  Example
  ```
  $ kubectl label nodes node-1 size=Large
  ```
  
![ln](images/ln.PNG)
  
- To create a pod definition
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
   name: myapp-pod
  spec:
   containers:
   - name: data-processor
     image: data-processor
   nodeSelector:
    size: Large
```
```bash
kubectl create -f pod-definition.yml
```
![nsel](images/nsel.PNG)

## Node Selector - Limitations
- We used a single label and selector to achieve our goal here. But what if our requirement is much more complex.
  
![nsl](images/nsl.PNG)
 
- For this we have **`Node Affinity and Anti Affinity`**


## Node Affinity

#### The primary feature of Node Affinity is to ensure that the pods are hosted on particular nodes.
- With **`Node Selectors`** we cannot provide the advance expressions.
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
   name: myapp-pod
  spec:
   containers:
   - name: data-processor
     image: data-processor
   nodeSelector:
    size: Large
```
![ns-old](images/ns-old.PNG)

```yaml
  apiVersion: v1
  kind: Pod
  metadata:
   name: myapp-pod
  spec:
   containers:
   - name: data-processor
     image: data-processor
   affinity:
     nodeAffinity:
       requiredDuringSchedulingIgnoredDuringExecution:
          nodeSelectorTerms:
          - matchExpressions:
            - key: size
              operator: In
              values: 
              - Large
              - Medium
```

![na](images/na.PNG)
  
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
   name: myapp-pod
  spec:
   containers:
   - name: data-processor
     image: data-processor
   affinity:
     nodeAffinity:
       requiredDuringSchedulingIgnoredDuringExecution:
          nodeSelectorTerms:
          - matchExpressions:
            - key: size
              operator: NotIn
              values: 
              - Small
```
![na1](images/na1.PNG)
  
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
   name: myapp-pod
  spec:
   containers:
   - name: data-processor
     image: data-processor
   affinity:
     nodeAffinity:
       requiredDuringSchedulingIgnoredDuringExecution:
          nodeSelectorTerms:
          - matchExpressions:
            - key: size
              operator: Exists
```

![na2](images/na2.PNG)

## Node Affinity Types
- Available
  - requiredDuringSchedulingIgnoredDuringExecution
  - preferredDuringSchedulingIgnoredDuringExecution
- Planned
  - requiredDuringSchedulingRequiredDuringExecution
  - preferredDuringSchedulingRequiredDuringExecution
  
  ![nat](images/nat.PNG)
  
## Node Affinity Types States

  ![nats](images/nats.PNG)
  
  ![nats1](images/nats1.PNG)
  

## Taints and Tolerations vs Node Affinity
- Taints and Tolerations do not guarantee that the pods will only prefer these nodes; in this case, the red pods may end up on one of the other nodes that do not have a taint or toleration set.
  
![tn-na](images/tn-na.PNG)
  
 
- As such, a combination of taints and tolerations and node affinity rules can be used together to completely dedicate nodes for specific parts.

![tn-nsa](images/tn-nsa.png)
  

## Resource Limits

#### Let us take a look at 3 node kubernetes cluster.
- Each node has a set of CPU, Memory and Disk resources available.
- If there is no sufficient resources available on any of the nodes, kubernetes holds the scheduling the pod. You will see the pod in pending state. If you look at the events, you will see the reason as insufficient CPU.
  
![rl](images/rl.PNG)
  
## Resource Requirements
- By default, K8s assume that a pod or container within a pod requires **`0.5`** CPU and **`256Mi`** of memory. 
- This is known as the **`Resource Request` for a container**.
  
![rr](images/rr.PNG)
  
- If your application within the pod requires more than the default resources, you need to set them in the pod definition file.

```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: simple-webapp-color
    labels:
      name: simple-webapp-color
  spec:
   containers:
   - name: simple-webapp-color
     image: simple-webapp-color
     ports:
      - containerPort:  8080
     resources:
       requests:
        memory: "1Gi"
        cpu: "1"
```
![rr-pod](images/rr-pod.PNG) 
   
## Resources - Limits
- By default, k8s sets resource limits to 1 CPU and 512Mi of memory
  
![rsl](images/rsl.PNG)
  
- You can set the resource limits in the pod definition file.
  
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: simple-webapp-color
    labels:
      name: simple-webapp-color
  spec:
   containers:
   - name: simple-webapp-color
     image: simple-webapp-color
     ports:
      - containerPort:  8080
     resources:
       requests:
        memory: "1Gi"
        cpu: "1"
       limits:
         memory: "2Gi"
         cpu: "2"
```
![rsl1](images/rsl1.PNG)
  
#### Note: Remember Requests and Limits for resources are set per container in the pod.
  
## Exceed Limits
- what happens when a pod tries to exceed resources beyond its limits?
- Whatever the limit set for CPU can not be exceed but in Memory if limit exceeds pod will be terminated OOM (Out Of Memory)

![el](images/el.PNG)

- Checkout for `king: LimitRange`
- hard limit set at namespace level using `kind: ResourceQuota`


## DaemonSets

#### DaemonSets are like replicasets, as it helps in to deploy multiple instances of pod. But it runs one copy of your pod on each node in your cluster.
  
![ds](images/ds.PNG)
  
## DaemonSets - UseCases

![ds-uc](images/ds-uc.PNG)
  
![ds-uc-kp](images/ds-uc-kp.PNG)
  
![ds-ucn](images/ds-ucn.PNG)
  
## DaemonSets - Definition
- Creating a DaemonSet is similar to the ReplicaSet creation process.
- For DaemonSets, we start with apiVersion, kind as **`DaemonSets`** instead of **`ReplicaSet`**, metadata and spec. 
- Some typical uses of a DaemonSet are:
  - running a cluster storage daemon on every node
  - running a logs collection daemon on every node
  - running a node monitoring daemon on every node

```yaml
  apiVersion: apps/v1
  kind: Replicaset
  metadata:
    name: monitoring-daemon
    labels:
      app: nginx
  spec:
    selector:
      matchLabels:
        app: monitoring-agent
    template:
      metadata:
       labels:
         app: monitoring-agent
      spec:
        containers:
        - name: monitoring-agent
          image: monitoring-agent
```
  
```yaml
  apiVersion: apps/v1
  kind: DaemonSet
  metadata:
    name: monitoring-daemon
    labels:
      app: nginx
  spec:
    selector:
      matchLabels:
        app: monitoring-agent
    template:
      metadata:
       labels:
         app: monitoring-agent
      spec:
        containers:
        - name: monitoring-agent
          image: monitoring-agent
```
![dsd](images/dsd.PNG)
  
- To create a daemonset from a definition file
```bash
kubectl create -f daemon-set-definition.yaml
```

## View DaemonSets
- To list daemonsets
```bash
kubectl get daemonsets
```
- For more details of the daemonsets
```bash
kubectl describe daemonsets monitoring-daemon
```
![ds1](images/ds1.PNG)
  
## How DaemonSets Works

![ds2](images/ds2.PNG)


## Static Pods 

#### How do you provide a pod definition file to the kubelet without a kube-apiserver?
- You can configure the kubelet to read the pod definition files from a directory on the server designated to store information about pods.

## Configure Static Pod
- The designated directory can be any directory on the host and the location of that directory is passed in to the kubelet as an option while running the service.
  - The option is named as **`--pod-manifest-path`**.
  
![sp](images/sp.PNG)
  
## Another way to configure static pod 
- Instead of specifying the option directly in the **`kubelet.service`** file, you could provide a path to another config file using the config option, and define the directory path as staticPodPath in the file.

![sp1](images/sp1.PNG)

## View the static pods
- To view the static pods
```bash
docker ps
```
![sp2](images/sp2.PNG)

#### The kubelet can create both kinds of pods - the static pods and the ones from the api server at the same time.

![sp3](images/sp3.PNG)

## Static Pods - Use Case

![sp4](images/sp4.PNG)
  
![sp5](images/sp5.PNG)
  
## Static Pods vs DaemonSets

   ![spvsds](images/spvsds.PNG)
  



# Logging and Monitoring Section Introduction  
In this section, we will take a look at the below
- Monitor Cluster Components
- Monitor Applications
- Monitor Cluster Components Logs
- Application Logs

## Monitor Cluster Components

#### How do you monitor resource consumption in kubernetes? or more importantly, what would you like to monitor?
![mon](images/mon.PNG)
 
## Heapster vs Metrics Server
- Heapster is now deprecated and a slimmed down version was formed known as the **`metrics server`**.

![hpms](images/hpms.PNG)
  
## Metrics Server

![ms1](images/ms1.PNG)

#### How are the metrics generated for the PODs on these nodes?

![ca](images/ca.PNG)
  
## Metrics Server - Getting Started
- One matrix server per cluster. Its store in memory but not store in disk.
- Kubelet contains cAdvisor is resposible for retriving performance metrix.

![msg](images/msg.PNG)
  
- Clone the metric server from github repo
```bash
git clone https://github.com/kubernetes-incubator/metrics-server.git
```
- Deploy the metric server
```bash
kubectl create -f metric-server/deploy/1.8+/
```
  
- View the cluster performance
```bash
kubectl top node
```
- View performance metrics of pod
```bash
kubectl top pod
```
  
![view](images/view.PNG)
  
  

## Managing Application Logs

#### Let us start with logging in docker

![ld](images/ld.PNG)
 
![ld1](images/ld1.PNG)
 
#### Logs - Kubernetes
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: event-simulator-pod
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
```

![logs-k8s](images/logs-k8s.png)
 
- To view the logs
```bash
kubectl logs -f event-simulator-pod
```
- If there are multiple containers in a pod then you must specify the name of the container explicitly in the command.
```bash
kubectl logs -f <pod-name> <container-name>
kubectl logs -f even-simulator-pod event-simulator
```

![logs1](images/logs1.PNG)
  

# Application Lifecycle Management Section Introduction

## Rolling Updates and Rollback
- create versioning of deployment
 kubectl rollout status deployment.yml

## Rollout and Versioning in a Deployment

![rollv](images/rollv.PNG)
  
## Rollout commands
- You can see the status of the rollout by the below command
  ```
  kubectl rollout status deployment/myapp-deployment
  ```
- To see the history and revisions
- To see the history and revisions
- To see the history and revisions
  ```
  kubectl rollout history deployment/myapp-deployment
  ```
 
![rollc](images/rollc.PNG)
  
## Deployment Strategies
- There are 2 types of deployment strategies
  1. Recreate
  2. RollingUpdate (Default Strategy)
  
![dst](images/dst.PNG)
  
## kubectl apply
- To update a deployment, edit the deployment and make necessary changes and save it. Then run the below command.

```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
   name: myapp-deployment
   labels:
    app: nginx
  spec:
   template:
     metadata:
       name: myap-pod
       labels:
         app: myapp
         type: front-end
     spec:
      containers:
      - name: nginx-container
        image: nginx:1.7.1
   replicas: 3
   selector:
    matchLabels:
      type: front-end       
```
```
  kubectl apply -f deployment-definition.yaml
```
- Alternate way to update a deployment say for example for updating an image.
```
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
```
![ka](images/ka.PNG)
  
## Recreate vs RollingUpdate
  
![rcrl](images/rcrl.PNG)
  
## Upgrades

![up](images/up.PNG)
  
## Rollback
  
![rb](images/rb.PNG)
  
- To undo a change
```
kubectl rollout undo deployment/myapp-deployment
```
  
## kubectl create
- To create a deployment
  ```
  $ kubectl create deployment nginx --image=nginx
  ```
## Summarize kubectl commands
```
$ kubectl create -f deployment-definition.yaml
$ kubectl get deployments
$ kubectl apply -f deployment-definition.yaml
$ kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
$ kubectl rollout status deployment/myapp-deployment
$ kubectl rollout history deployment/myapp-deployment
$ kubectl rollout undo deployment/myapp-deployment
```

![sum](images/sum.PNG)
 



## Configure Environment Variables In Applications
  
#### ENV variables in Docker
```
$ docker run -e APP_COLOR=pink simple-webapp-color
```

#### ENV variables in kubernetes 
- To set an environment variable set an **`env`** property in pod definition file.
  
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: simple-webapp-color
  spec:
   containers:
   - name: simple-webapp-color
     image: simple-webapp-color
     ports:
     - containerPort: 8080
     env:
     - name: APP_COLOR
       value: pink
  ```
  ![env](images/env.PNG)
  
- There are other ways of setting the environment variables such as **`ConfigMaps`** and **`Secrets`**

  ![cms](images/cms.PNG)
  


## Configure ConfigMaps in Applications


## ConfigMaps
- There are 2 phases involved in configuring ConfigMaps. 
  - First, create the configMaps
  - Second, Inject then into the pod.
- There are 2 ways of creating a configmap.
  - The Imperative way
    ```
    $ kubectl create configmap app-config --from-literal=APP_COLOR=blue --from-literal=APP_MODE=prod
    $ kubectl create configmap app-config --from-file=app_config.properties (Another way)
    ```
    ![cmi](images/cmi.PNG)
    
  - The Declarative way
    
    ```
    apiVersion: v1
    kind: ConfigMap
    metadata:
     name: app-config
    data:
     APP_COLOR: blue
     APP_MODE: prod
    ```
    ```
    Create a config map definition file and run the 'kubectl create` command to deploy it.
    $ kubectl create -f config-map.yaml
    ```
    ![cmd1](images/cmd1.PNG)
    
 ## View ConfigMaps
 - To view configMaps
   ```
   $ kubectl get configmaps (or)
   $ kubectl get cm
   ```
 - To describe configmaps
   ```
   $ kubectl describe configmaps
   ```
   
   ![cmv](images/cmv.PNG)
   
 ## ConfigMap in Pods
 - Inject configmap in pod
   ```
   apiVersion: v1
   kind: Pod
   metadata:
     name: simple-webapp-color
   spec:
    containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
      - containerPort: 8080
      envFrom:
      - configMapRef:
          name: app-config
   ```
   ```
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: app-config
   data:
     APP_COLOR: blue
     APP_MODE: prod
   ```
   ```
   $ kubectl create -f pod-definition.yaml
   ```
  
   ![cmp](images/cmp.PNG)
   
 #### There are other ways to inject configuration variables into pod   
 - You can inject it as a **`Single Environment Variable`** 
 - You can inject it as a file in a **`Volume`**
 
   ![cmp1](images/cmp1.PNG)
   


## Secrets
  - Take me to [Video Tutorials](https://kodekloud.com/topic/secrets-2/)

In this section, we will take a look at secrets in kubernetes

## Web-Mysql Application

 ![web](images/web.PNG)
 
- One way is to move the app properties/envs into a configmap. But the configmap stores data into a plain text format. 
- It is definitely not a right place to store a password.
  ```
  apiVersion: v1
  kind: ConfigMap
  metadata:
   name: app-config
  data:
    DB_Host: mysql
    DB_User: root
    DB_Password: paswrd
  ```
  ![web1](images/web1.PNG)
  
- Secrets are used to store sensitive information. 
- They are similar to configmaps but they are stored in an encrypted format or a hashed format.

#### There are 2 steps involved with secrets
- First, Create a secret
- Second, Inject the secret into a pod.
  
  ![sec](images/sec.PNG)
  
#### There are 2 ways of creating a secret
- The Imperative way
  ```
  $ kubectl create secret generic app-secret --from-literal=DB_Host=mysql --from-literal=DB_User=root --from-literal=DB_Password=paswrd
  $ kubectl create secret generic app-secret --from-file=app_secret.properties
  ```
  ![csi](images/csi.PNG)
  
- The Declarative way
  ```
  Generate a hash value of the password and pass it to secret-data.yaml definition value as a value to DB_Password variable.
  $ echo -n "mysql" | base64
  $ echo -n "root" | base64
  $ echo -n "paswrd"| base64
  ```
  
  Create a secret definition file and run `kubectl create` to deploy it
  ```
  apiVersion: v1
  kind: Secret
  metadata:
   name: app-secret
  data:
    DB_Host: bX1zcWw=
    DB_User: cm9vdA==
    DB_Password: cGFzd3Jk
  ```
  ```
  $ kubectl create -f secret-data.yaml
  ```

  ![csd](images/csd.PNG)
  
## Encode Secrets

  ![enc](images/enc.PNG)
  
## View Secrets
- To view secrets
  ```
  $ kubectl get secrets
  ```
- To describe secret
  ```
  $ kubectl describe secret
  ```
- To view the values of the secret
  ```
  $ kubectl get secret app-secret -o yaml
  ```
  
  ![secv](images/secv.PNG)
  
## Decode Secrets
- To decode secrets
  ```
  $ echo -n "bX1zcWw=" | base64 --decode
  $ echo -n "cm9vdA==" | base64 --decode
  $ echo -n "cGFzd3Jk" | base64 --decode
  ```
  ![secd](images/secd.PNG)
  
## Configuring secret with a pod
- To inject a secret to a pod add a new property **`envFrom`** followed by **`secretRef`** name and then create the pod-definition
  
  ```
  apiVersion: v1
  kind: Secret
  metadata:
   name: app-secret
  data:
    DB_Host: bX1zcWw=
    DB_User: cm9vdA==
    DB_Password: cGFzd3Jk
  ```
  ```
   apiVersion: v1
   kind: Pod
   metadata:
     name: simple-webapp-color
   spec:
    containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
      - containerPort: 8080
      envFrom:
      - secretRef:
          name: app-secret
   ```
  ```
  $ kubectl create -f pod-definition.yaml
  ```
  ![secp](images/secp.PNG)
  
#### There are other ways to inject secrets into pods.
- You can inject as **`Single ENV variable`**
- You can inject as whole secret as files in a **`Volume`**

  ![seco](images/seco.PNG)
  
## Secrets in pods as volume
- Each attribute in the secret is created as a file with the value of the secret as its content.
  
  ![secpv](images/secpv.PNG)

  


## Multi-Container Pods


## Monolith and Microservices

  ![loga](images/loga.PNG)
  
#### Multi-Container Pods

  ![mcp](images/mcp.PNG)
  
- To create a new multi-container pod, add the new container information to the pod definition file.
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: simple-webapp
    labels:
      name: simple-webapp
  spec:
    containers:
    - name: simple-webapp
      image: simple-webapp
      ports:
      - ContainerPort: 8080
    - name: log-agent
      image: log-agent
  ```
  ![mcpc](images/mcpc.PNG)
 

## Multi-Container Pods Design Patterns
  
  ![dp](images/dp.PNG)
  


## Init-Containers

  
#### K8s Reference Docs
- https://kubernetes.io/docs/concepts/workloads/pods/init-containers/
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/



# Cluster Maintenance Section Introduction
In this section, we will take a look at cluster maintenance
- Cluster Upgrade Process
- Operating System Upgrades
- Backup and Restore Methodologies

## OS Upgrades
#### If the node was down for more than 5 minutes, then the pods are terminated from that node

![os](images/os.PNG)
  
- You can purposefully **`drain`** the node of all the workloads so that the workloads are moved to other nodes.

```
kubectl drain node-1
```
- The node is also cordoned or marked as unschedulable.
- When the node is back online after a maintenance, it is still unschedulable. You then need to uncordon it.
```
kubectl uncordon node-1
```
- There is also another command called cordon. Cordon simply marks a node unschedulable. Unlike drain it does not terminate or move the pods on an existing node.

![drain](images/drain.PNG)
  
  
#### K8s Reference Docs
- https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/



## Kubernetes Software Versions
  
In this section, we will take a look at various kubernetes releases and versions

#### We can see the kubernetess version that we installed
```
$ kubectl get nodes
```
![kgn](images/kgn.PNG)

#### Let's take a closer look at the version number
- It consists of 3 parts
  - First is the major version
  - Second is the minor version
  - Finally, the patch version
  
  ![mmp](images/mmp.PNG)
  
#### Kubernetes follows a standard software release versioning procedure
- You can find all kubernetes releases at https://github.com/kubernetes/kubernetes/releases

  ![r1](images/r1.PNG)
  
  ![r2](images/r2.PNG)
  
#### Downloaded package has all the kubernetes components in it except **`ETCD Cluster`** and **`CoreDNS`** as they are seperate projects.

 ![r3](images/r3.PNG)
 
 
 
## Cluster Upgrade Introduction
  
#### Is it mandatory for all of the kubernetes components to have the same versions?
- No, The components can be at different release versions.
  
#### At any time, kubernetes supports only up to the recent 3 minor versions
- The recommended approach is to upgrade one minor version at a time.
  
  ![up2](images/up2.PNG)
  
#### Options to upgrade k8s cluster
 
  ![opt](images/opt.PNG)
  
## Upgrading a Cluster
- Upgrading a cluster involves 2 major steps
  
#### There are different strategies that are available to upgrade the worker nodes
- One is to upgrade all at once. But then your pods will be down and users will not be able to access the applications.
  ![stg1](images/stg1.PNG)
- Second one is to upgrade one node at a time. 
  ![stg2](images/stg2.PNG)
- Third one would be to add new nodes to the cluster
  ![stg3](images/stg3.PNG)
  
## kubeadm - Upgrade master node
- kubeadm has an upgrade command that helps in upgrading clusters.
  ```
  $ kubeadm upgrade plan
  ```
  ![kube1](images/kube1.png)
  
- Upgrade kubeadm from v1.11 to v1.12
  ```
  $ apt-get upgrade -y kubeadm=1.12.0-00
  ```
- Upgrade the cluster
  ```
  $ kubeadm upgrade apply v1.12.0
  ```
- If you run the 'kubectl get nodes' command, you will see the older version. This is because in the output of the command it is showing the versions of kubelets on each of these nodes registered with the API Server and not the version of API Server itself  
  ```
  $ kubectl get nodes
  ```
  
  ![kubeu](images/kubeu.PNG)
  
- Upgrade 'kubelet' on the master node
  ```
  $ apt-get upgrade kubelet=1.12.0-00
  ```
- Restart the kubelet
  ```
  $ systemctl restart kubelet
  ```
- Run 'kubectl get nodes' to verify
  ```
  $ kubectl get nodes
  ```
  
  ![kubeu1](images/kubeu1.PNG)
 
## kubeadm - Upgrade worker nodes
  
- From master node, run 'kubectl drain' command to move the workloads to other nodes
  ```
  $ kubectl drain node-1
  ```
- Upgrade kubeadm and kubelet packages
  ```
  $ apt-get upgrade -y kubeadm=1.12.0-00
  $ apt-get upgrade -y kubelet=1.12.0-00
  ```
- Update the node configuration for the new kubelet version
  ```
  $ kubeadm upgrade node config --kubelet-version v1.12.0
  ```
- Restart the kubelet service
  ```
  $ systemctl restart kubelet
  ```
- Mark the node back to schedulable
  ```
  $ kubectl uncordon node-1
  ```
  
  ![kubeu2](images/kubeu2.PNG)
  
- Upgrade all worker nodes in the same way

  ![kubeu3](images/kubeu3.PNG)
  

## Backup and Restore Methods
In this section, we will take a look at backup and restore methods

## Backup Candidates
 
 ![bc](images/bc.PNG)
 
## Resource Configuration
- Imperative way
  
  ![rci](images/rci.PNG)

- Declarative Way (Preferred approach)
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp-pod
    labels:
      app: myapp
      type: front-end
  spec:
    containers:
    - name: nginx-container
      image: nginx
  ```
 ![rcd](images/rcd.PNG)
 
- A good practice is to store resource configurations on source code repositories like github.

  ![rcd1](images/rcd1.PNG)

## Backup - Resource Configs

  ```
  $ kubectl get all --all-namespaces -o yaml > all-deploy-services.yaml (only for few resource groups)
  ```

- There are many other resource groups that must be considered. There are tools like **`ARK`** or now called **`Velero`** by Heptio that can do this for you.

  ![brc](images/brc.PNG)
  
## Backup - ETCD
- So, instead of backing up resources as before, you may choose to backup the ETCD cluster itself. 
  
  ![be](images/be.PNG)
  
- You can take a snapshot of the etcd database by using **`etcdctl`** utility snapshot save command.
  ```
  $ ETCDCTL_API=3 etcdctl snapshot save snapshot.db
  ```
  ```
  $  ETCDCTL_API=3 etcdctl snapshot status snapshot.db
  ```
  ![be1](images/be1.PNG)
  
## Restore - ETCD
- To restore etcd from the backup at later in time. First stop kube-apiserver service
  ```
  $ service kube-apiserver stop
  ```
- Run the etcdctl snapshot restore command
- Update the etcd service
- Reload system configs
  ```
  $ systemctl daemon-reload
  ```
- Restart etcd
  ```
  $ service etcd restart
  ```
  
  ![er](images/er.PNG)
  
- Start the kube-apiserver
  ```
  $ service kube-apiserver start
  ```
#### With all etcdctl commands specify the cert,key,cacert and endpoint for authentication.
```
$ ETCDCTL_API=3 etcdctl \
  snapshot save /tmp/snapshot.db \
  --endpoints=https://[127.0.0.1]:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/etcd-server.crt \
  --key=/etc/kubernetes/pki/etcd/etcd-server.key
```

  ![erest](images/erest.PNG)
  
#### K8s Reference Docs
- https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/


# Security Section Introduction
In this section, we will take a look at security section introduction
- Kubernetes Security Primitives
- Authentication
- TLS certificates for cluster components
- Secure Persistent key-value store
- Authorization
- Images Security
- Security Contexts
- Network Policies   

## Kubernetes Security Primitives
  
In this section, we will take a look at kubernetes security primitives

## Secure Hosts

 ![sech](images/sech.PNG)
  
## Secure Kubernetes
- We need to make two types of decisions.
  - Who can access?
  - What can they do?
 
  ![seck](images/seck.PNG)
  
## Authentication
- Who can access the API Server is defined by the Authentication mechanisms.
  - Files: - Username and Passwords
  - Files - Username and Tockens
  - certificates
  - External autthentication providers - LDAP
  - Service Accounts
  
## Authorization
- Once they gain access to the cluster, what they can do is defined by authorization mechanisms.
  - RBAC Autherization
  - ABAC Autherization
  - Node Autherization
  - Webhook mode

## TLS Certificates
- All communication with the cluster, between the various components such as the ETCD Cluster, kube-controller-manager, scheduler, api server, as well as those running on the working nodes such as the kubelet and kubeproxy is secured using TLS encryption.

 ![tls](images/tls.PNG)
 
## Network Policies
What about communication between applications within the cluster?

  ![np](images/np.PNG)
  
# Authentication

In this section, we will take a look at authentication in a kubernetes cluster

  ![auth1](images/auth1.PNG)

## Accounts  
- Different users that may be accessing the cluster security of end users who access the applications deployed on the cluster is managed by the applications themselves internally.

 ![acc1](images/acc1.PNG)
 
- So, we left with 2 types of users
  - Humans, such as the Administrators and Developers
  - Robots such as other processes/services or applications that require access to the cluster.
  

![acc2](images/acc2.PNG)
  
- All user access is managed by apiserver and all of the requests goes through apiserver.
 
![acc3](images/acc3.PNG)
  
## Authentication Mechanisms
- There are different authentication mechanisms that can be configured.

![auth2](images/auth2.PNG)
  
## Authentication Mechanisms - Basic
  
![auth3](images/auth3.PNG)
  
## kube-apiserver configuration
- If you set up via kubeadm then update kube-apiserver.yaml manifest file with the option.
  
  ![auth4](images/auth4.PNG)
  
## Authenticate User

- To authenticate using the basic credentials while accessing the API server specify the username and password in a curl command.
  ```
  $ curl -v -k http://master-node-ip:6443/api/v1/pods -u "user1:password123"
  ```
![auth5](images/auth5.PNG)
  
- We can have additional column in the user-details.csv file to assign users to specific groups.

![auth6](images/auth6.PNG)
  
## Note
 
![note](images/note.PNG)
  
  
#### K8s Reference Docs
- https://kubernetes.io/docs/reference/access-authn-authz/authentication/ 
  
 
## TLS Certificates Introduction
  
In this section, we will take a look at TLS certificates
- What are TLS certificates?
- How does kubernetes use certificates?
- How to generate them?
- How to configure them?
- How to view them?
- How to troubleshoot issues related to certificates

## TLS Basics
  
In this section, we will take a look at TLS Basics

### Certificate
- A certificate is used to guarantee trust between 2 parties during a transaction.
- Example: when a user tries to access web server, tls certificates ensure that the communication between them is encrypted.

![cert1](images/cert1.PNG)
  
  
## Symmetric Encryption
- It is a secure way of encryption, but it uses the `same key to encrypt and decrypt` the data and the key has to be exchanged between the sender and the receiver, there is a risk of a hacker gaining access to the key and decrypting the data.

![cert2](images/cert2.PNG)
  
## Asymmetric Encryption
- Instead of using single key to encrypt and decrypt data, asymmetric encryption uses a pair of keys, a private key and a public key.

![cert3](images/cert3.PNG)
  
![cert4](images/cert4.PNG)
  
![cert5](images/cert5.PNG)
  
![cert6](images/cert6.PNG)
  

#### How do you look at a certificate and verify if it is legit?
- who signed and issued the certificate.
- If you generate the certificate then you will have it sign it by yourself; that is known as self-signed certificate.

![cert7](images/cert7.PNG)
  
#### How do you generate legitimate certificate? How do you get your certificates singed by someone with authority?
- That's where **`Certificate Authority (CA)`** comes in for you. Some of the popular ones are Symantec, DigiCert, Comodo, GlobalSign etc.

![cert8](images/cert8.PNG)
  
![cert9](images/cert9.PNG)
  
![cert10](images/cert10.PNG)
  
## Public Key Infrastructure
   
![pki](images/pki.PNG)
   
## Certificates naming convention

![cert11](images/cert11.PNG)
  
  
## TLS in Kubernetes
  
In this section, we will take a look at TLS in kubernetes

#### The two primary requirements are to have all the various services within the cluster to use server certificates and all clients to use client certificates to verify they are who they say they are.
- Server Certificates for Servers
- Client Certificates for Clients

![tls](images/tls.PNG)
  
#### Let's look at the different components within the k8s cluster and identify the various servers and clients and who talks to whom.

![certs](images/certs.PNG)
  

## TLS in kubernetes - Certificate Creation
In this section, we will take a look at TLS certificate creation in kubernetes

## Generate Certificates
- There are different tools available such as easyrsa, openssl or cfssl etc. or many others for generating certificates.

## Certificate Authority (CA)

- Generate Keys
```bash
openssl genrsa -out ca.key 2048
```
- Generate CSR
```bash
openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr
```
- Sign certificates
```bash
openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
```
 
![ca1](images/ca1.PNG)
 
## Generating Client Certificates

#### Admin User Certificates

- Generate Keys
  ```
  $ openssl genrsa -out admin.key 2048
  ```
- Generate CSR
  ```
  $ openssl req -new -key admin.key -subj "/CN=kube-admin" -out admin.csr
  ```
- Sign certificates
  ```
  $ openssl x509 -req -in admin.csr -CA ca.crt -CAkey ca.key -out admin.crt
  ```
  
  ![ca2](images/ca2.PNG)
  
- Certificate with admin privilages
  ```
  $ openssl req -new -key admin.key -subj "/CN=kube-admin/O=system:masters" -out admin.csr
  ```
  
#### We follow the same procedure to generate client certificate for all other components that access the kube-apiserver.

  ![crt1](images/crt1.PNG)
  
  ![crt2](images/crt2.PNG)
  
  ![crt3](images/crt3.PNG)
   
  ![crt4](images/crt4.PNG)
  
## Generating Server Certificates

## ETCD Server certificate

![etc1](images/etc1.PNG)
  
![etc2](images/etc2.PNG)
  
## Kube-apiserver certificate

![api1](images/api1.PNG)
  
![api2](images/api2.PNG)
  
## Kubectl Nodes (Server Cert)

![kctl1](images/kctl1.PNG)
   
## Kubectl Nodes (Client Cert)

![kctl2](images/kctl2.PNG)
   
   
   
## View Certificate Details
  
In this section, we will take a look how to view certificates in a kubernetes cluster.

## View Certs 
![hrd](images/hrd.PNG)

![hrd1](images/hrd1.PNG)
 
 - To view the details of the certificate
```bash
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
```
   
![hrd2](images/hrd2.PNG)
   
#### Follow the same procedure to identify information about of all the other certificates

![hrd3](images/hrd3.PNG)
   
## Inspect Server Logs - Hardware setup
- Inspect server logs using journalctl
```bash
journalctl -u etcd.service -l
```
  
![hrd4](images/hrd4.PNG)
  
## Inspect Server Logs - kubeadm setup
- View logs using kubectl
```bash
kubectl logs etcd-master
```
![hrd5](images/hrd5.PNG)
  
- View logs using docker ps and docker logs
```bash
docker ps -a
docker logs <container-id>
```
![hrd6](images/hrd6.PNG)
  
#### K8s Reference Docs
- https://kubernetes.io/docs/setup/best-practices/certificates/#certificate-paths
  
  
## Certificate API  
In this section, we will take a look at how to manage certificates and certificate API's in kubernetes

## CA (Certificate Authority)
- The CA is really just the pair of key and certificate files that we have generated, whoever gains access to these pair of files can sign any certificate for the kubernetes environment.

#### Kubernetes has a built-in certificates API that can do this for you. 
- With the certificate API, we now send a certificate signing request (CSR) directly to kubernetes through an API call.
   
![csr](images/csr.PNG)
   
#### This certificate can then be extracted and shared with the user.
- A user first creates a key
```bash
openssl genrsa -out jane.key 2048
```
- Generates a CSR
```bash
openssl req -new -key jane.key -subj "/CN=jane" -out jane.csr 
```
```bash
cat jane.csr | base64
```
- Sends the request to the administrator and the adminsitrator takes the key and creates a CSR object, with kind as "CertificateSigningRequest" and a encoded "jane.csr"

```yaml
  apiVersion: certificates.k8s.io/v1beta1
  kind: CertificateSigningRequest
  metadata:
    name: jane
  spec:
    groups:
    - system:authenticated
    usages:
    - digital signature
    - key encipherment
    - server auth
    request:
      <certificate-goes-here base64 cert>
```
```bash 
kubectl create -f jane.yaml
```
![csr1](images/csr1.PNG)
  
- To list the csr's
  ```
  $ kubectl get csr
  ```
- Approve the request
  ```
  $ kubectl certificate approve jane
  ```
- To view the certificate
  ```
  $ kubectl get csr jane -o yaml
  ```
- To decode it
  ```
  $ echo "<certificate>" |base64 --decode
  ```
  ![csr2](images/csr2.PNG)
  
#### All the certificate releated operations are carried out by the controller manager.
- If anyone has to sign the certificates they need the CA Servers, root certificate and private key. The controller manager configuration has two options where you can specify this.

![csr3](images/csr3.PNG)
  
![csr4](images/csr4.PNG)
  
  
#### K8s Reference Docs
- https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/
- https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/
 
  
## KubeConfig 

In this section, we will take a look at kubeconfig in kubernetes

#### Client uses the certificate file and key to query the kubernetes Rest API for a list of pods using curl.
- You can specify the same using kubectl

![kc1](images/kc1.PNG)
  
- We can move these information to a configuration file called kubeconfig. And the specify this file as the kubeconfig option in the command.
```bash
kubectl get pods --kubeconfig config
```
  
## Kubeconfig File
- The kubeconfig file has 3 sections
  - Clusters
  - Contexts
  - Users
  
![kc4](images/kc4.PNG)
  
![kc5](images/kc5.PNG)
  
- To view the current file being used
  ```
  $ kubectl config view
  ```
- You can specify the kubeconfig file with kubectl config view with "--kubeconfig" flag
  ```
  $ kubectl config veiw --kubeconfig=my-custom-config
  ```
  
  ![kc6](images/kc6.PNG)
  
- How do you update your current context? Or change the current context
  ```
  $ kubectl config view --kubeconfig=my-custom-config
  ```
  
  ![kc7](images/kc7.PNG)
  
- kubectl config help
  ```
  $ kubectl config -h
  ```
  
  ![kc8](images/kc8.PNG)
  
## What about namespaces?

  ![kc9](images/kc9.PNG)
 
## Certificates in kubeconfig

  ![kc10](images/kc10.PNG)
 
  ![kc12](images/kc12.PNG)
  
  ![kc11](images/kc11.PNG)
 
#### K8s Reference Docs
- https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config



## API Groups
  
In this section, we will take a look at API Groups in kubernetes

## To return version and list pods via API's 

![api3](images/api3.PNG)
 
- The kubernetes API is grouped into multiple such groups based on their purpose. Such as one for **`APIs`**, one for **`healthz`**, **`metrics`** and **`logs`** etc.

  ![api4](images/api4.PNG)
 
## API and APIs
- These APIs are catagorized into two.
  - The core group - Where all the functionality exists
    
    ![api5](images/api5.PNG)
 
  - The Named group - More organized and going forward all the newer features are going to be made available to these named groups.
  
    ![api6](images/api6.PNG)
    
- To list all the api groups

  ![api7](images/api7.PNG)
  
## Note on accessing the kube-apiserver
- You have to authenticate by passing the certificate files.

  ![api8](images/api8.PNG)
  
- An alternate is to start a **`kubeproxy`** client
  
  ![api9](images/api9.PNG)
  
## kube proxy vs kubectl proxy
 
  ![kp](images/kp.PNG)
  
## Key Takeaways

  ![api10](images/api10.PNG)

#### K8s Reference Docs
- https://kubernetes.io/docs/concepts/overview/kubernetes-api/
- https://kubernetes.io/docs/reference/using-api/api-concepts/
- https://kubernetes.io/docs/tasks/extend-kubernetes/http-proxy-access-api/


## Authorization
In this section, we will take a look at authorization in kubernetes

## Why do you need Authorization in your cluster?
- As an admin, you can do all operations
```bash
kubectl get nodes
kubectl get pods
kubectl delete node worker-2
```
  
![at1](images/at1.PNG)
  
## Authorization Mechanisms
- There are different authorization mechanisms supported by kubernetes
  - Node Authorization
  - Attribute-based Authorization (ABAC)
  - Role-Based Authorization (RBAC)
  - Webhook
  
## Node Authorization

  ![node-auth](images/node-auth.png)
  
## ABAC

  ![abac](images/abac.PNG)
  
## RBAC

  ![rbac](images/rbac.PNG)

## Webhook
  
  ![webhook](images/webhook.PNG)
  
## Authorization Modes
- The mode options can be defined on the kube-apiserver

  ![mode](images/mode.PNG)
  
- When you specify multiple modes, it will authorize in the order in which it is specified

  ![mode1](images/mode1.PNG)
  
  
  #### K8s Reference Docs
  - https://kubernetes.io/docs/reference/access-authn-authz/authorization/
  

## RBAC
In this section, we will take a look at RBAC

## How do we create a role?
- Each role has 3 sections
  - apiGroups
  - resources
  - verbs
- create the role with kubectl command
```bash
kubectl create -f developer-role.yaml
```

## The next step is to link the user to that role.
- For this we create another object called **`RoleBinding`**. This role binding object links a user object to a role.
- create the role binding using kubectl command
```bash
kubectl create -f devuser-developer-binding.yaml
```
- Also note that the roles and role bindings fall under the scope of namespace.
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: Role
  metadata:
    name: developer
  rules:
  - apiGroups: [""] # "" indicates the core API group
    resources: ["pods"]
    verbs: ["get", "list", "update", "delete", "create"]
  - apiGroups: [""]
    resources: ["ConfigMap"]
    verbs: ["create"]
  ```
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: RoleBinding
  metadata:
    name: devuser-developer-binding
  subjects:
  - kind: User
    name: dev-user # "name" is case sensitive
    apiGroup: rbac.authorization.k8s.io
  roleRef:
    kind: Role
    name: developer
    apiGroup: rbac.authorization.k8s.io
  ```
  ![rbac1](images/rbac1.PNG)
  

## View RBAC
  
- To list roles
```bash
 kubectl get roles
```
- To list rolebindings
```bash
kubectl get rolebindings
```
- To describe role 
```bash
kubectl describe role developer
```
  
![rbac2](images/rbac2.PNG)
    
- To describe rolebinding
```bash
kubectl describe rolebinding devuser-developer-binding
```
  
![rbac3](images/rbac3.PNG)
  
#### What if you being a user would like to see if you have access to a particular resource in the cluster.
## Check Access

- You can use the kubectl auth command
```bash
kubectl auth can-i create deployments
kubectl auth can-i delete nodes
```
```bash
kubectl auth can-i create deployments --as dev-user
kubectl auth can-i create pods --as dev-user
```
```
kubectl auth can-i create pods --as dev-user --namespace test
```
  
![rbac5](images/rbac5.PNG)
  
## Resource Names
- Note on resource names we just saw how you can provide access to users for resources like pods within the namespace.

```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: Role
  metadata:
    name: developer
  rules:
  - apiGroups: [""] # "" indicates the core API group
    resources: ["pods"]
    verbs: ["get", "update", "create"]
    resourceNames: ["blue", "orange"]
```  
![rbac4](images/rbac4.PNG)
  
#### K8s Reference Docs
- https://kubernetes.io/docs/reference/access-authn-authz/rbac/
- https://kubernetes.io/docs/reference/access-authn-authz/rbac/#command-line-utilities



# Cluster Roles
 
In this section, we will take a look at cluster roles

## Roles
- Roles and Rolebindings are namespaced meaning they are created within namespaces.
  
![roles](images/roles.PNG)
  
## Namespaces
- Can you group or isolate nodes within  a namespace?
  - No, those are cluster wide or cluster scoped resources. They cannot be associated to any particular namespace.
  
![namespace](images/namespace.PNG)
  
- So the resources are categorized as either namespaced or cluster scoped.
  
- To see namespaced resources
```bash
kubectl api-resources --namespaced=true
```
- To see non-namespaced resources
```bash
kubectl api-resources --namespaced=false
```
  
![namespace1](images/namespace1.PNG)
  
## Cluster Roles and Cluster Role Bindings
- Cluster Roles are roles except they are for a cluster scoped resources. Kind as **`CLusterRole`** 
```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    name: cluster-administrator
  rules:
  - apiGroups: [""] # "" indicates the core API group
    resources: ["nodes"]
    verbs: ["get", "list", "delete", "create"]
```
```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRoleBinding
  metadata:
    name: cluster-admin-role-binding
  subjects:
  - kind: User
    name: cluster-admin
    apiGroup: rbac.authorization.k8s.io
  roleRef:
    kind: ClusterRole
    name: cluster-administrator
    apiGroup: rbac.authorization.k8s.io
```
```bash
kubectl create -f cluster-admin-role.yaml
kubectl create -f cluster-admin-role-binding.yaml
```
  
![cr1](images/cr1.PNG)
  
- You can create a cluster role for namespace resources as well. When you do that user will have access to these resources across all namespaces.


# Service Account

- The user account is used by humans, and service accounts are used by machines.

- A service account could be an account used by an application to interact with a Kubernetes cluster.

- For example, a monitoring application like Prometheus uses a service account to pull the Kubernetes API for performance metrics.

- An automated build tool like Jenkins uses service accounts to deploy applications on the Kubernetes cluster.


# Image Security

In this section we will take a look at image security

## Image
   
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx-pod
  spec:
    containers:
    - name: nginx
      image: nginx
```
  
  ![img1](images/img1.PNG)
  
  ![img2](images/img2.PNG)
  
## Private Registry
- To login to the registry
  ```
  $ docker login private-registry.io
  ```
- Run the application using the image available at the private registry
  ```
  $ docker run private-registry.io/apps/internal-app
  ```
  
![prvr](images/prvr.PNG)
  
- To pass the credentials to the docker untaged on the worker node for that we first create a secret object with credentials in it.
```bash
kubectl create secret docker-registry regcred \
    --docker-server=private-registry.io \ 
    --docker-username=registry-user \
    --docker-password=registry-password \
    --docker-email=registry-user@org.com
```
- We then specify the secret inside our pod definition file under the imagePullSecret section 
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx-pod
  spec:
    containers:
    - name: nginx
      image: private-registry.io/apps/internal-app
    imagePullSecrets:
    - name: regcred
```
![prvr1](images/prvr1.PNG)
  
#### K8s Reference Docs
  - https://kubernetes.io/docs/concepts/containers/images/




## Security Context
  
In this section, we will take a look at security context

## Container Security
 ```
 $ docker run --user=1001 ubuntu sleep 3600
 $ docker run -cap-add MAC_ADMIN ubuntu
 ```
 
 ![csec](images/csec.PNG)
 
## Kubernetes Security
- You may choose to configure the security settings at a container level or at a pod level.

 ![ksec](images/ksec.PNG)

## Security Context
- To add security context on the container and a field called **`securityContext`** under the spec section.

```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: web-pod
  spec:
    securityContext:
      runAsUser: 1000
    containers:
    - name: ubuntu
      image: ubuntu
      command: ["sleep", "3600"]
```
  ![sxc1](images/sxc1.PNG)
  
- To set the same context at the container level, then move the whole section under container section.
  
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: web-pod
  spec:
    containers:
    - name: ubuntu
      image: ubuntu
      command: ["sleep", "3600"]
      securityContext:
        runAsUser: 1000
```
![sxc2](images/sxc2.PNG)
  
- To add capabilities use the **`capabilities`** option
```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: web-pod
  spec:
    containers:
    - name: ubuntu
      image: ubuntu
      command: ["sleep", "3600"]
      securityContext:
        runAsUser: 1000
        capabilities: 
          add: ["MAC_ADMIN"]
```
![cap](images/cap.PNG)
  
  


# Network Policies
  
#### Trafic flowing through a webserver serving frontend to users an app server serving backend API and a database server

  ![traffic](images/traffic.PNG)
  
- There are two types of traffic
  - Ingress
  - Egress
  
![ing1](images/ing1.PNG)
  
![ing2](images/ing2.PNG)
  
## Network Security

![nsec](images/nsec.PNG)
  
## Network Policy

![npol](images/npol.PNG)
  
![npol1](images/npol1.PNG)
  
## Network Policy Selectors
  
![npolsec](images/npolsec.PNG)
  
## Network Policy Rules

![npol2](images/npol2.PNG)
  
## Create network policy
 
- To create a network policy
```yaml
  apiVersion: networking.k8s.io/v1
  kind: NetworkPolicy
  metadata:
   name: db-policy
  spec:
    podSelector:
      matchLabels:
        role: db
    policyTypes:
    - Ingress
    ingress:
    - from:
      - podSelector:
          matchLabels:
            role: api-pod
      ports:
      - protocol: TCP
        port: 3306
```
  
```
kubectl create -f policy-definition.yaml
```
  
![npol3](images/npol3.PNG)
 
![npol4](images/npol4.PNG)
  
## Note
 
![note1](images/note1.PNG)



# Volumes
## Persistent Volumes

In this section, we will take a look at **Persistent Volumes**

- In the large evnironment, with a lot of users deploying a lot of pods, the users would have to configure storage every time for each Pod.
- Whatever storage solution is used, the users who deploys the pods would have to configure that on all pod definition files in his environment. Every time a change is to be made, the user would have to make them on all of his pods.

![class-16](images/class16.PNG)


- A Persistent Volume is a cluster-wide pool of storage volumes configured by an administrator to be used by users deploying application on the cluster. 
- The users can now select storage from this pool using Persistent Volume Claims.

```yaml
  pv-definition.yaml
  
  kind: PersistentVolume
  apiVersion: v1
  metadata:
    name: pv-vol1
  spec:
    accessModes: [ "ReadWriteOnce" ]
    capacity:
     storage: 1Gi
    hostPath:
     path: /tmp/data
```

```bash
  $ kubectl create -f pv-definition.yaml
  persistentvolume/pv-vol1 created

  $ kubectl get pv
  NAME      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
  pv-vol1   1Gi        RWO            Retain           Available                                   3min
  
  $ kubectl delete pv pv-vol1
  persistentvolume "pv-vol1" deleted
```


## Persistent Volume Claims

In this section, we will take a look at **Persistent Volume Claim**

- Now we will create a Persistent Volume Claim to make the storage available to the node.
- Volumes and Persistent Volume Claim are two separate objects in the Kubernetes namespace.
- Once the Persistent Volume Claim created, Kubernetes binds the Persistent Volumes to claim based on the request and properties set on the volume.


![class-17](images/class17.PNG)

- If properties not matches or Persistent Volume is not available for the Persistent Volume Claim then it will display the pending state.

```yaml
pvc-definition.yaml

kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: myclaim
spec:
  accessModes: [ "ReadWriteOnce" ]
  resources:
   requests:
     storage: 1Gi
```

```yaml
pv-definition.yaml

kind: PersistentVolume
apiVersion: v1
metadata:
    name: pv-vol1
spec:
    accessModes: [ "ReadWriteOnce" ]
    capacity:
     storage: 1Gi
    hostPath:
     path: /tmp/data
```

#### Create the Persistent Volume

```
$ kubectl create -f pv-definition.yaml
persistentvolume/pv-vol1 created

$ kubectl get pv
NAME      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
pv-vol1   1Gi        RWO            Retain           Available                                   10s
```


#### Create the Persistent Volume Claim

```
$ kubectl create -f pvc-definition.yaml
persistentvolumeclaim/myclaim created

$ kubectl get pvc
NAME      STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
myclaim   Pending                                                     35s

$ kubectl get pvc
NAME      STATUS   VOLUME    CAPACITY   ACCESS MODES   STORAGECLASS   AGE
myclaim   Bound    pv-vol1   1Gi        RWO                           1min

```

#### Delete the Persistent Volume Claim

```
$ kubectl delete pvc myclaim
```

#### Delete the Persistent Volume

```
$ kubectl delete pv pv-vol1
```


#### Kubernetes Persistent Volume Claims Reference Docs

- https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims
- https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#persistentvolumeclaim-v1-core
- https://docs.cloud.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengcreatingpersistentvolumeclaim.htm


## Using PVC in PODs

In this section, we will take a look at **Using PVC in PODs**

- In this case, Pods access storage by using the claim as a volume. Persistent Volume Claim must exist in the same namespace as the Pod using the claim. 
- The cluster finds the claim in the Pod's namespace and uses it to get the Persistent Volume backing the claim. The volume is then mounted to the host and into the Pod.
- Persistent Volume is a cluster-scoped and Persistent Volume Claim is a namespace-scoped.

#### Create the Persistent Volume

```yaml
pv-definition.yaml

kind: PersistentVolume
apiVersion: v1
metadata:
    name: pv-vol1
spec:
    accessModes: [ "ReadWriteOnce" ]
    capacity:
     storage: 1Gi
    hostPath:
     path: /tmp/data
```
```
$ kubectl create -f pv-definition.yaml

```

#### Create the Persistent Volume Claim

```yaml
pvc-definition.yaml

kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: myclaim
spec:
  accessModes: [ "ReadWriteOnce" ]
  resources:
   requests:
     storage: 1Gi
```
```
$ kubectl create -f pvc-definition.yaml
```

#### Create a Pod

```yaml
pod-definition.yaml

apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: web
  volumes:
    - name: web
      persistentVolumeClaim:
        claimName: myclaim
```
```
$ kubectl create -f pod-definition.yaml

```

#### List the Pod,Persistent Volume and Persistent Volume Claim

```
$ kubectl get pod,pvc,pv

```

#### References Docs

- https://kubernetes.io/docs/concepts/storage/persistent-volumes/#claims-as-volumes


```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    hostPath:
      # directory location on host
      path: /var/log/webapp
      # this field is optional
      type: Directory
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-log
spec:
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 100Mi
  hostPath:
    path: /pv/log
```

     
```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: claim-log-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 50Mi
```
  
```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: claim-log-1
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 50Mi
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    persistentVolumeClaim:
      claimName: claim-log-1
```

## Storage Class

In this section, we will take a look at **Storage Class**

- We discussed about how to create Persistent Volume and Persistent Volume Claim and We also saw that how to use into the Pod's volume to claim that volume space.
- We created Persistent Volume but before this if we are taking a volume from Cloud providers like GCP, AWS, Azure. We need to first create disk in the Google Cloud as an example. 
- We need to create manually each time when we define in the Pod definition file. that's called **Static Provisioning**. 

#### Static Provisioning

![class-18](images/class18.PNG)


#### Dynamic Provisioning

![class-19](images/class19.PNG)

- No we have a Storage Class, So we no longer to define Persistent Volume. It will create automatically when a Storage Class is created. It's called **Dynamic Provisioning**. 

```bash
vi sc-definition.yaml
```
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
   name: google-storage
provisioner: kubernetes.io/gce-pd
```

#### Create a Storage Class

```bash
kubectl create -f sc-definition.yaml
storageclass.storage.k8s.io/google-storage created
```

#### List the Storage Class

```bash
kubectl get sc
NAME             PROVISIONER            RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
google-storage   kubernetes.io/gce-pd   Delete          Immediate           false                  20s
```

#### Create a Persistent Volume Claim

```yaml
pvc-definition.yaml

kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: myclaim
spec:
  accessModes: [ "ReadWriteOnce" ]
  storageClassName: google-storage       
  resources:
   requests:
     storage: 500Mi
```
```bash
$ kubectl create -f pvc-definition.yaml

```
#### Create a Pod

```yaml
pod-definition.yaml

apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: frontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: web
  volumes:
    - name: web
      persistentVolumeClaim:
        claimName: myclaim
```
```bash
kubectl create -f pod-definition.yaml
```
#### Provisioner

![class-20](images/class20.PNG)

## Ingress

In this section, we will take a look at **Ingress**

- Ingress Controller
- Ingress Resources

## Ingress Controller

- Deployment of **Ingress Controller**

## ConfigMap

```
kind: ConfigMap
apiVersion: v1
metadata:
  name: nginx-configuration
```

## Deployment

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ingress-controller
spec:
  replicas: 1
  selector:
    matchLabels:
      name: nginx-ingress
  template:
    metadata:
      labels:
        name: nginx-ingress
    spec:
      serviceAccountName: ingress-serviceaccount
      containers:
        - name: nginx-ingress-controller
          image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.21.0
          args:
            - /nginx-ingress-controller
            - --configmap=$(POD_NAMESPACE)/nginx-configuration
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: http
              containerPort: 80
            - name: https
              containerPort: 443
```

## ServiceAccount

- ServiceAccount require for authentication purposes along with correct Roles, ClusterRoles and RoleBindings.

- Create a ingress service account
```
$ kubectl create -f ingress-sa.yaml
serviceaccount/ingress-serviceaccount created
```

## Service Type - NodePort

```
# service-Nodeport.yaml

apiVersion: v1
kind: Service
metadata:
  name: ingress
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    protocol: TCP
    name: http
  - port: 443
    targetPort: 443
    protocol: TCP
    name: https
  selector:
    name: nginx-ingress
```

- Create a service
```
$ kubectl create -f service-Nodeport.yaml
```
- To get the service

```
$ kubectl get service
```

## Ingress Resources

```
Ingress-wear.yaml

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear
spec:
     backend:
        serviceName: wear-service
        servicePort: 80
```

- To create the ingress resource
```
$ kubectl create -f Ingress-wear.yaml
ingress.extensions/ingress-wear created
```

- To get the ingress
```
$ kubectl get ingress
NAME           CLASS    HOSTS   ADDRESS   PORTS   AGE
ingress-wear   <none>   *                 80      18s
```

## Ingress Resource - Rules

- 1 Rule and 2 Paths.

```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear-watch
spec:
  rules:
  - http:
      paths:
      - path: /wear
        backend:
          serviceName: wear-service
          servicePort: 80
      - path: /watch
        backend:
          serviceName: watch-service
          servicePort: 80
```
- Describe the earlier created ingress resource

```
$ kubectl describe ingress ingress-wear-watch
Name:             ingress-wear-watch
Namespace:        default
Address:
Default backend:  default-http-backend:80 (<none>)
Rules:
  Host        Path  Backends
  ----        ----  --------
  *
              /wear    wear-service:80 (<none>)
              /watch   watch-service:80 (<none>)
Annotations:  <none>
Events:
  Type    Reason  Age   From                      Message
  ----    ------  ----  ----                      -------
  Normal  CREATE  23s   nginx-ingress-controller  Ingress default/ingress-wear-watch

```

- 2 Rules and 1 Path each.
```
# Ingress-wear-watch.yaml

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear-watch
spec:
  rules:
  - host: wear.my-online-store.com
    http:
      paths:
      - backend:
          serviceName: wear-service
          servicePort: 80
  - host: watch.my-online-store.com
    http:
      paths:
      - backend:
          serviceName: watch-service
          servicePort: 80
```


#### References Docs

- https://kubernetes.io/docs/concepts/services-networking/ingress/
- https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/
- https://thenewstack.io/kubernetes-ingress-for-beginners/


## Ingress Annotations and rewrite-target

In this section, we will take a look at **Ingress annotations and rewrite-target**

- Different Ingress controllers have different options to customize the way it works. Nginx Ingress Controller has many options but we will take a look into the one of the option "Rewrite Target" option.

- Kubernetes Version 1.18

```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  namespace: critical-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /pay
        backend:
          serviceName: pay-service
          servicePort: 8282

```

#### Reference Docs

- https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/
- https://kubernetes.github.io/ingress-nginx/examples/
- https://kubernetes.github.io/ingress-nginx/examples/rewrite/
- https://github.com/kubernetes/ingress-nginx/blob/master/docs/troubleshooting.md

## Kubernetes Commands
Command | Explanation
--------|-------------
`kubectl get nodes` | List all nodes in the cluster.
`kubectl get pods` | List all pods in the default namespace.
`kubectl get pods -n my-namespace` | List all pods in a specific namespace.
`kubectl get pods -o jsonpath={.items[*].metadata.name}` | List the names of all pods using jsonpath. 
`kubectl describe node my-node` | Detailed information about a specific node.
`kubectl describe pod my-pod` | Detailed information about a specific pod.
`kubectl logs my-pod` | Print the logs for a specific pod.
`kubectl exec my-pod -- date` | Execute a command in a specific pod (e.g., print current date).
`kubectl run my-pod --image=my-image` | Run a specific image in a new pod.
`kubectl delete pod my-pod` | Delete a specific pod.
`kubectl create -f my-config.yaml` | Create resources defined in a specific YAML file.
`kubectl apply -f my-config.yaml` | Apply changes to resources defined in a specific YAML file.
`kubectl delete -f my-config.yaml` | Delete resources defined in a specific YAML file.
`kubectl get services` | List all services in the default namespace.
`kubectl get services -n my-namespace` | List all services in a specific namespace.
`kubectl get deployments` | List all deployments in the default namespace.
`kubectl get deployments -n my-namespace` | List all deployments in a specific namespace.
`kubectl scale --replicas=3 deployment/my-deployment` | Scale a deployment to 3 replicas.
`kubectl rollout status deployment/my-deployment` | Check the rollout status of a specific deployment.
`kubectl rollout undo deployment/my-deployment` | Roll back the last update to a specific deployment.

## Errors in K8 & how to troubleshoot them
- Kubernetes, like any complex system, can encounter various errors and issues during setup, configuration, and runtime. Here are 20 common errors in Kubernetes and ways to troubleshoot them:
### 1. Error: Unable to connect to the cluster
Troubleshooting:
-  Verify your kubectl configuration using kubectl config view.
-  Ensure that the cluster API server is accessible from your machine.
-  Check if the cluster is running (kubectl cluster-info).
#### 2. Error: ImagePullBackOff or ErrImagePull
Troubleshooting:
- Verify the image name and repository.
-  Check image availability and permissions.
-  Ensure network connectivity to the container registry.
####  3. Error: CrashLoopBackOff
Troubleshooting:
-  Check pod logs (kubectl logs <pod_name>).
-  Inspect the pod's events (kubectl describe pod <pod_name>).
-  Verify resource constraints and application health.
#### 4. Error: PersistentVolumeClaim is pending
Troubleshooting:
-  Check storage class availability and status.
-  Verify storage provider configuration.
-  Ensure sufficient storage capacity in the cluster.

#### 5. Error: Pod stays in Pending state
Troubleshooting:
-  Check if there are enough resources in the cluster.
-  Inspect pod events and describe the pod (kubectl describe pod <pod_name>).
-  Examine the node's status and resource availability.

#### 6. Error: Service is not accessible
Troubleshooting:
-  Verify service configuration and ports.
-  Check firewall rules and network policies.
-  Ensure that the service selector matches pod labels.
#### 7. Error: Unauthorized (RBAC-related issues)
Troubleshooting:
-  Verify your user's RBAC permissions.
-  Check roles and role bindings (kubectl get roles, kubectl get rolebindings).
-  Ensure proper context and authentication settings in kubectl.
#### 8. Error: Node NotReady
Troubleshooting:
- Check if kubelet is running on the node.
- Verify node status (kubectl get nodes).
- Examine kubelet logs for errors.
#### 9. Error: Insufficient CPU or Memory
Troubleshooting:
- Check resource requests and limits in pod specs.
- Verify node capacity and resource utilization.
- Examine pod events and describe the pod.
#### 10. Error: NamespaceNotFound
Troubleshooting:
- Ensure the specified namespace exists.
- Check your current context (kubectl config current-context).
#### 11. Error: ConfigMap or Secret not found
Troubleshooting:
- Verify the resource name and namespace.
- Check if the resource was created (kubectl get configmaps).
#### 12. Error: DNS Resolution Issues
Troubleshooting:
- Verify CoreDNS or kube-dns pods are running.
- Check DNS configuration in pods.
- Ensure that the service and pod names are correct.
#### 13. Error: Invalid YAML Syntax
Troubleshooting:
- Use YAML linters to validate your configuration.
- Double-check indentation and syntax.
- Inspect error messages for specific details.
#### 14. Error: NodeSelector does not match nodes
Troubleshooting:
- Check node labels and selectors in pod specifications.
- Verify that nodes match the required labels.
#### 15. Error: Unable to access external services
Troubleshooting:
- Check network policies and firewall rules.
- Verify external service availability.
- Examine service endpoint configurations.
#### 16. Error: ResourceQuota Exceeded
Troubleshooting:
- Check resource quotas and limits for namespaces.
- Verify resource utilization in the cluster.
#### 17. Error: Ingress Controller Misconfiguration
Troubleshooting:
- Check Ingress resource for syntax errors.
- Verify Ingress controller logs.
- Ensure proper annotations and backend services.
#### 18. Error: Custom Resource Definition (CRD) Not Found
Troubleshooting:
- Check if the CRD is installed (kubectl get crds).
- Verify API group and version.
#### 19. Error: Unable to create LoadBalancer Service
Troubleshooting:
- Verify cloud provider credentials.
- Check if LoadBalancer services are supported in your environment.
#### 20. Error: Node Affinity or Anti-Affinity Issues
Troubleshooting:
- Check node affinity or anti-affinity rules in pod specifications.
- Verify that nodes have the required labels.

#### 
- When troubleshooting Kubernetes issues, it's essential to use a systematic approach, inspect logs, and make use of Kubernetes resources like kubectl describe, kubectl logs, and kubectl get. Additionally, monitoring tools and observability solutions can provide insights into the cluster's health and performance. 
- Always refer to the official Kubernetes documentation for detailed troubleshooting guidance.


https://www.youtube.com/watch?v=M4X4Fpq2Xl8&list=PLlLpHNj8iPU9SULfEQiw2JrwEihiQEzY0


Sandeep@gracia_309


### Stateful set not shifting to a new node

- This is by design. 
- When a node goes "down", the master does not know whether it was a safe down (deliberate shutdown) or a network partition. 
- Thus PVC with that node remains on the same node and master mark the pods on that node as `Unknown`

- By default, Kubernetes always try to create pod on the same node where PVC is provisioned, which is the reason the pod always comes up on the same node when deleted.

- This `PVC` goes onto other node only when you `cordon the node`, `drain the node` and delete the node from cluster, 
- Now master knows this node doesn't exist in cluster. 
- Hence master moves PVC to another node and pod comes up on that node.

