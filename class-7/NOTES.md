Project ID: cc-2026-johornsby
Project number: 992439028444

Suffix: jhorns01

Image: fastapi
Digest: sha256:fa3acbc471d24e512b70a0521caae9e50bd5cef9b647c3d12636cd8247382842

    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl apply -f k8s
    deployment.apps/fastapi created
    service/fastapi created
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl rollout status deployment/fastapi --timeout=10m
    Waiting for deployment "fastapi" rollout to finish: 0 of 1 updated replicas are available...
    deployment "fastapi" successfully rolled out
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl get pods -l app=fastapi
    NAME                       READY   STATUS    RESTARTS   AGE
    fastapi-5549cfb54d-p97nl   1/1     Running   0          27s
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl get service fastapi
    NAME      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
    fastapi   ClusterIP   34.118.234.46   <none>        80/TCP    36s
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl port-forward service/fastapi 8080:80
    Forwarding from 127.0.0.1:8080 -> 8080
    Handling connection for 8080
    Handling connection for 8080
    Handling connection for 8080
    Handling connection for 8080
    ^Cjho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl apply -f k8s/deployment.yaml
    deployment.apps/fastapi configured
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl rollout status deployment/fastapi --timeout=10m
    Waiting for deployment "fastapi" rollout to finish: 1 of 2 updated replicas are available...
    deployment "fastapi" successfully rolled out
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl get pods -l app=fastapi -o wide
    NAME                       READY   STATUS    RESTARTS   AGE   IP             NODE                                               NOMINATED NODE   READINESS GATES
    fastapi-5549cfb54d-kp9vd   1/1     Running   0          18s   10.86.128.16   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    fastapi-5549cfb54d-p97nl   1/1     Running   0          11m   10.86.128.15   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl get endpointslices -l kubernetes.io/service-name=fastapi
    NAME            ADDRESSTYPE   PORTS   ENDPOINTS                   AGE
    fastapi-wgmr4   IPv4          8080    10.86.128.15,10.86.128.16   11m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ 

Prediction:
* Number of ready pods will temporarily drop to 1/2
* The Service will keep the same CLUSTER-IP

d

    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl config current-context
    gke_cc-2026-johornsby_europe-west1-b_lab7-gke-jhorns01
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get deployment fastapi
    NAME      READY   UP-TO-DATE   AVAILABLE   AGE
    fastapi   2/2     2            2           22m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get pods -l app=fastapi -o wide
    NAME                       READY   STATUS    RESTARTS   AGE   IP             NODE                                               NOMINATED NODE   READINESS GATES
    fastapi-5549cfb54d-kp9vd   1/1     Running   0          11m   10.86.128.16   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    fastapi-5549cfb54d-p97nl   1/1     Running   0          22m   10.86.128.15   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get service fastapi
    NAME      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
    fastapi   ClusterIP   34.118.234.46   <none>        80/TCP    22m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$


d

    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl config current-context
    gke_cc-2026-johornsby_europe-west1-b_lab7-gke-jhorns01
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubctl -n default get deployment fastapi
    -bash: kubctl: command not found
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get deployment fastapi
    NAME      READY   UP-TO-DATE   AVAILABLE   AGE
    fastapi   2/2     2            2           21m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get pods -l app=fastapi -o wide
    NAME                       READY   STATUS    RESTARTS   AGE   IP             NODE                                               NOMINATED NODE   READINESS GATES
    fastapi-5549cfb54d-kp9vd   1/1     Running   0          10m   10.86.128.16   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    fastapi-5549cfb54d-p97nl   1/1     Running   0          21m   10.86.128.15   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get service fastapi
    NAME      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
    fastapi   ClusterIP   34.118.234.46   <none>        80/TCP    21m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl config current-context
    gke_cc-2026-johornsby_europe-west1-b_lab7-gke-jhorns01
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get deployment fastapi
    NAME      READY   UP-TO-DATE   AVAILABLE   AGE
    fastapi   2/2     2            2           22m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get pods -l app=fastapi -o wide
    NAME                       READY   STATUS    RESTARTS   AGE   IP             NODE                                               NOMINATED NODE   READINESS GATES
    fastapi-5549cfb54d-kp9vd   1/1     Running   0          11m   10.86.128.16   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    fastapi-5549cfb54d-p97nl   1/1     Running   0          22m   10.86.128.15   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get service fastapi
    NAME      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
    fastapi   ClusterIP   34.118.234.46   <none>        80/TCP    22m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ ^C
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ OLD_POD=^C
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ OLD_POD=fastapi-5549cfb54d-p97nl
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default delete pod "$OLD_POD" --wait=false
    pod "fastapi-5549cfb54d-p97nl" deleted from default namespace
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get pods -l app=fastapi --watch
    NAME                       READY   STATUS    RESTARTS   AGE
    fastapi-5549cfb54d-kp9vd   1/1     Running   0          13m
    fastapi-5549cfb54d-nsp2r   0/1     Running   0          5s
    fastapi-5549cfb54d-nsp2r   1/1     Running   0          13s
    fastapi-5549cfb54d-nsp2r   1/1     Running   0          13s
    ^Cjho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get pods -l app=fastapi -o wide
    NAME                       READY   STATUS    RESTARTS   AGE   IP             NODE                                               NOMINATED NODE   READINESS GATES
    fastapi-5549cfb54d-kp9vd   1/1     Running   0          13m   10.86.128.16   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    fastapi-5549cfb54d-nsp2r   1/1     Running   0          61s   10.86.128.17   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d   <none>           <none>
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default get service fastapi
    NAME      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
    fastapi   ClusterIP   34.118.234.46   <none>        80/TCP    25m
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl -n default describe endpointslices -l kubernetes.io/service-name=fastapi
    Name:         fastapi-wgmr4
    Namespace:    default
    Labels:       endpointslice.kubernetes.io/managed-by=endpointslice-controller.k8s.io
                kubernetes.io/service-name=fastapi
    Annotations:  endpoints.kubernetes.io/last-change-trigger-time: 2026-11-22T17:46:44Z
    AddressType:  IPv4
    Ports:
    Name  Port  Protocol
    ----  ----  --------
    http  8080  TCP
    Endpoints:
    - Addresses:  10.86.128.16
        Conditions:
        Ready:    true
        Hostname:   <unset>
        TargetRef:  Pod/fastapi-5549cfb54d-kp9vd
        NodeName:   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d
        Zone:       europe-west1-b
    - Addresses:  10.86.128.17
        Conditions:
        Ready:    true
        Hostname:   <unset>
        TargetRef:  Pod/fastapi-5549cfb54d-nsp2r
        NodeName:   gke-lab7-gke-jhorns01-default-pool-d03ffdf7-w06d
        Zone:       europe-west1-b
    Events:         <none>
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ 

"In one or two sentences, explain which resource restored the replica count and why a client can still use the same Service address."

    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl describe deployment fastapi
    Name:                   fastapi
    Namespace:              default
    CreationTimestamp:      Sun, 22 Nov 2026 17:22:20 +0000
    Labels:                 <none>
    Annotations:            autopilot.gke.io/resource-adjustment:
                            {"input":{"containers":[{"limits":{"cpu":"250m","memory":"512Mi"},"requests":{"cpu":"250m","memory":"512Mi"},"name":"fastapi"}]},"output":...
                            autopilot.gke.io/warden-version: 37.9.0-gke.3
                            deployment.kubernetes.io/revision: 1
    Selector:               app=fastapi
    Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
    StrategyType:           RollingUpdate
    MinReadySeconds:        0
    RollingUpdateStrategy:  25% max unavailable, 25% max surge
    Pod Template:
    Labels:  app=fastapi
    Containers:
    fastapi:
        Image:      europe-west1-docker.pkg.dev/cc-2026-johornsby/lab7-containers-jhorns01/fastapi:v1
        Port:       8080/TCP (http)
        Host Port:  0/TCP (http)
        Limits:
        cpu:                250m
        ephemeral-storage:  1Gi
        memory:             512Mi
        Requests:
        cpu:                250m
        ephemeral-storage:  1Gi
        memory:             512Mi
        Liveness:             http-get http://:http/health delay=0s timeout=1s period=10s successThreshold=1 failureThreshold=3
        Readiness:            http-get http://:http/health delay=0s timeout=1s period=10s successThreshold=1 failureThreshold=3
        Environment:          <none>
        Mounts:               <none>
    Volumes:                <none>
    Node-Selectors:         <none>
    Tolerations:            kubernetes.io/arch=amd64:NoSchedule
    Conditions:
    Type           Status  Reason
    ----           ------  ------
    Progressing    True    NewReplicaSetAvailable
    Available      True    MinimumReplicasAvailable
    OldReplicaSets:  <none>
    NewReplicaSet:   fastapi-5549cfb54d (2/2 replicas created)
    Events:
    Type    Reason             Age   From                   Message
    ----    ------             ----  ----                   -------
    Normal  ScalingReplicaSet  39m   deployment-controller  Scaled up replica set fastapi-5549cfb54d from 0 to 1
    Normal  ScalingReplicaSet  28m   deployment-controller  Scaled up replica set fastapi-5549cfb54d from 1 to 2
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ curl http://localhost:8080; echo
    Handling connection for 8080
    {"message":"Hello from FastAPI on Kubernetes"}
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ curl http://localhost:8080; echo
    Handling connection for 8080
    {"message":"Hello from FastAPI on Kubernetes"}
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl apply -f k8s/deployment.yaml 
    deployment.apps/fastapi configured
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl rollout status deployment/fastapi --timeout=10m
    Waiting for deployment "fastapi" rollout to finish: 1 out of 2 new replicas have been updated...
    Waiting for deployment "fastapi" rollout to finish: 1 out of 2 new replicas have been updated...
    Waiting for deployment "fastapi" rollout to finish: 1 out of 2 new replicas have been updated...
    Waiting for deployment "fastapi" rollout to finish: 1 old replicas are pending termination...
    Waiting for deployment "fastapi" rollout to finish: 1 old replicas are pending termination...
    Waiting for deployment "fastapi" rollout to finish: 1 old replicas are pending termination...
    deployment "fastapi" successfully rolled out
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl get replicasets -l app=fastapi
    NAME                 DESIRED   CURRENT   READY   AGE
    fastapi-5549cfb54d   0         0         0       41m
    fastapi-868c56b9     2         2         2       34s
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl describe deployment fastapi
    Name:                   fastapi
    Namespace:              default
    CreationTimestamp:      Sun, 22 Nov 2026 17:22:20 +0000
    Labels:                 <none>
    Annotations:            autopilot.gke.io/resource-adjustment:
                            {"input":{"containers":[{"limits":{"cpu":"250m","memory":"512Mi"},"requests":{"cpu":"250m","memory":"512Mi"},"name":"fastapi"}]},"output":...
                            autopilot.gke.io/warden-version: 37.9.0-gke.3
                            deployment.kubernetes.io/revision: 2
    Selector:               app=fastapi
    Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
    StrategyType:           RollingUpdate
    MinReadySeconds:        0
    RollingUpdateStrategy:  25% max unavailable, 25% max surge
    Pod Template:
    Labels:  app=fastapi
    Containers:
    fastapi:
        Image:      europe-west1-docker.pkg.dev/cc-2026-johornsby/lab7-containers-jhorns01/fastapi:v2
        Port:       8080/TCP (http)
        Host Port:  0/TCP (http)
        Limits:
        cpu:                250m
        ephemeral-storage:  1Gi
        memory:             512Mi
        Requests:
        cpu:                250m
        ephemeral-storage:  1Gi
        memory:             512Mi
        Liveness:             http-get http://:http/health delay=0s timeout=1s period=10s successThreshold=1 failureThreshold=3
        Readiness:            http-get http://:http/health delay=0s timeout=1s period=10s successThreshold=1 failureThreshold=3
        Environment:          <none>
        Mounts:               <none>
    Volumes:                <none>
    Node-Selectors:         <none>
    Tolerations:            kubernetes.io/arch=amd64:NoSchedule
    Conditions:
    Type           Status  Reason
    ----           ------  ------
    Available      True    MinimumReplicasAvailable
    Progressing    True    NewReplicaSetAvailable
    OldReplicaSets:  fastapi-5549cfb54d (0/0 replicas created)
    NewReplicaSet:   fastapi-868c56b9 (2/2 replicas created)
    Events:
    Type    Reason             Age   From                   Message
    ----    ------             ----  ----                   -------
    Normal  ScalingReplicaSet  41m   deployment-controller  Scaled up replica set fastapi-5549cfb54d from 0 to 1
    Normal  ScalingReplicaSet  30m   deployment-controller  Scaled up replica set fastapi-5549cfb54d from 1 to 2
    Normal  ScalingReplicaSet  48s   deployment-controller  Scaled up replica set fastapi-868c56b9 from 0 to 1
    Normal  ScalingReplicaSet  34s   deployment-controller  Scaled down replica set fastapi-5549cfb54d from 2 to 1
    Normal  ScalingReplicaSet  34s   deployment-controller  Scaled up replica set fastapi-868c56b9 from 1 to 2
    Normal  ScalingReplicaSet  22s   deployment-controller  Scaled down replica set fastapi-5549cfb54d from 1 to 0
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ curl http://localhost:8080; echo
    Handling connection for 8080
    E1122 18:04:37.004480    3898 portforward.go:549] "An error occurred forwarding" err="error forwarding port 8080 to pod d6347c86c794f11da9f8d0ed3f491801e090ce325ffa255a7b8f7f643a65f685, uid : failed to find sandbox \"d6347c86c794f11da9f8d0ed3f491801e090ce325ffa255a7b8f7f643a65f685\" in store: not found" localPort=8080
    remotePort=8080
    curl: (52) Empty reply from server
    error: lost connection to pod

    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ fg
    -bash: fg: job has terminated
    [1]+  Exit 1                  kubectl port-forward service/fastapi 8080:80
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl port-forward service/fastapi 8080:80 &
    [1] 4308
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ Forwarding from 127.0.0.1:8080 -> 8080

    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ curl http://localhost:8080; echo
    Handling connection for 8080
    {"message":"Hello from FastAPI v2 on Kubernetes"}
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ 

d

jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ EXTERNAL_IP=35.205.2.84
jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ RUN_ID=$(date +%s)

    for request in {1..20}; do
    curl --fail --silent --show-error --max-time 10 \
        --output /dev/null --write-out '%{http_code}\n' \
        "http://${EXTERNAL_IP}/health?lab7-check=${RUN_ID}-${request}"
    done
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    200
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$ kubectl logs -l app=fastapi --prefix=true --tail=-1 \
    | grep -F "lab7-check=${RUN_ID}-" \
    | awk '{print $1}' \
    | sort | uniq -c
        11 [pod/fastapi-868c56b9-6kjk5/fastapi]
        9 [pod/fastapi-868c56b9-pvtxf/fastapi]
    jho_recruitment@cloudshell:~/week7-cc/class-7/lab (cc-2026-johornsby)$
