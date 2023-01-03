# Kubernetes Commands

## Pods

* Get all pods - `kubectl get pods`
* Get all pods with more details - `kubectl get pods -o wide`
* Create a pod based on an image - `kubectl run nginx --image=nginx`
* See details of a pad by name - `kubectl describe pod podname`
* Delete a pod using pod name - `kubectl delete pod webapp`
* Generate a pod yaml file using the image type and output it to a `redis.yaml` file - `kubectl run redis --image=redis --dry-run=client -o yaml > redis.yaml`. The output of this command is:
    ```yaml
    apiVersion: v1
    kind : Pod
    metadata:
        creationTimestamp: null
        labels:
            run: redis
        name: redis
    spec:
        containers:
          - image: redis
            name: redis
            resources: {}
        dnsPolicy: ClusterFirst
        restartPolicy: Always
    status: {}
    ```

* Create a pod using a yaml file - `kubectl create -f redis.yaml`
* Apply modified pod yaml changes to an already created pod - `kubectl apply -f redis.yaml`

## Replication Controller and ReplicaSets

*  Contents of a Replication Controller yaml file
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
                specs:
                    containers:
                      - name: nginx-container
                        image: nginx
        replicas: 3
    ```

* Creating a ReplicationController using a yaml file - `kubectl create -f rc-defination.yml`
* Get all replication controllers - `kubectl get replicationcontroller`