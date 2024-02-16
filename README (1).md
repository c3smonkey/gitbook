---
description: '- Raspberry Pi Kubernetes Cluster with k3s -'
cover: .gitbook/assets/rpi-k3s-cluster.jpeg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# MiniIO - Kubernetes Cluster

First, add the Minio Helm chart repository:

```
helm repo add minio https://charts.min.io/
```

Next, install _MiniIO_ using _Helm_ with the desired configuration options:

```
helm install --set resources.requests.memory=512Mi --set replicas=1 --set persistence.enabled=false --set mode=standalone --set rootUser=rootuser,rootPassword=rootpass123 --generate-name minio/minio
```

After installation, you should see output similar to the following:

```
NAME: minio-1693079426
LAST DEPLOYED: Sat Aug 26 21:50:26 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
MinIO can be accessed via port 9000 on the following DNS name from within your cluster:
minio-1693079426.default.svc.cluster.local

To access MinIO from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace default -l "release=minio-1693079426" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace default

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access the MinIO server on http://localhost:9000. Follow the below steps to connect to the MinIO server with the mc client:

  1. Download the MinIO mc client - https://min.io/docs/minio/linux/reference/minio-mc.html#quickstart

  2. export MC_HOST_minio-1693079426-local=http://$(kubectl get secret --namespace default minio-1693079426 -o jsonpath="{.data.rootUser}" | base64 --decode):$(kubectl get secret --namespace default minio-1693079426 -o jsonpath="{.data.rootPassword}" | base64 --decode)@localhost:9000

  3. mc ls minio-1693079426-local
```

To access _MinIO_ from localhost, you can run the following commands:

```
export POD_NAME=$(kubectl get pods --namespace default -l "release=minio-1693079426" -o jsonpath="{.items[0].metadata.name}")
kubectl port-forward $POD_NAME 9000 --namespace default
```

You can retrieve the _root user_ and _password_ by running these commands:

```
kubectl get secret minio-1693079426 -o jsonpath="{.data.rootUser}" | base64 --decode
kubectl get secret minio-1693079426 -o jsonpath="{.data.rootPassword}" | base64 --decode
```

You can find the release name by running `helm list`:

```
helm list
NAME            	NAMESPACE	REVISION	UPDATED                              	STATUS  	CHART       	APP VERSION
minio-1693079426	default  	1       	2023-08-26 21:50:26.549651 +0200 CEST	deployed	minio-5.0.13	RELEASE.2023-07-07T07-13-57Z
```
