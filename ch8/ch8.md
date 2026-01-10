# Chapter 8 - Deployment, Replication Controller and ReplicaSet Explained

## Replication

Replication: spin up multiple identical instances of a pod.

Replication controller = pod1 + pod2 + pod3 ...

- can redirect traffic towards the pods it controls
- can span multiple nodes -> if resources of one node are not enough 

ReplicaSet is the new version of the ReplicationController(legacy)

`kubectl explain rs` -> explain Replica set
`kubectl explain rc` -> explain Replication controller

Edit the live yaml object: `kubectl edit rs/nginx-rs`

Scale the ReplicaSet imperatively

`kubectl scale --replicas=10 rs/nginx-rs`

## Deployment

How to update container image from 1.1 to 1.2 without downtime? Use deployments:

- rolling deployments -> create the new pods alongside the old ones and replace the old ones gradually
- rollback

A deployment is almost always more preferrable than a ReplicaSet. When creating a Deployment, Kubernetes creates internally a ReplicaSet to manage the pods


`kubectl get all` -> return all the objects in the cluster

`kubect set image deploy/nginx-deployment nginx=nginx:1.9.1` -> change the image on the deployment

`kubectl rollout history deploy/nginx-deployment` -> get history of the changes

`kubectl rollout undo deploy/nginx-deployment` -> performs the rollback of the latest change

`kubectl create deploy deploy/nginx-new --image=nginx --dry-run=client -o yaml > deploy.yaml`