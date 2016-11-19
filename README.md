# InfluxDB & Grafana using Kubernetes on Google Cloud Platform

~work in progress~

A simple demonstration of running InfluxDB and Grafana on Google Cloud Platform. Persistent disks are used for both InfluxDB and Grafana. Note that a higher performance disk (e.g. SSD) may be required for InfluxDB for some applications.

Within the Kubernetes cluster InfluxDB will be accessible at `http://influxdb:8086`, and Grafana can be accessed in your web browser at `https://<master ip>/api/v1/proxy/namespaces/default/services/grafana/`

## Setup InfluxDB
Create a persistent disk to be used as the storage for the InfluxDB data & metadata:
```
gcloud compute disks create influxdb --size=200GB --zone=europe-west1-c
```
Create a persistent volume:
```
kubectl create -f pv/influxdb.yaml
```
Create a persistent volume claim:
```
kubectl create -f pvc/influxdb.yaml
```
Create the InfluxDB deployment:
```
kubectl create -f deployments/influxdb.yaml
```
Create the InfluxDB service:
```
kubectl create -f services/influxdb.yaml
```
You can use `kubectl exec` to access a shell in the InfluxDB container and run the InfluxDB CLI, e.g.
```
$ kubectl exec influxdb-967644454-rwmqi -i -t -- bash -il
root@influxdb-967644454-rwmqi:/# influx
Visit https://enterprise.influxdata.com to register for updates, InfluxDB server management, and monitoring.
Connected to http://localhost:8086 version 1.1.0
InfluxDB shell version: 1.1.0
>
```
This makes it easy to add an admin user, create other users, add databases etc.

## Setup Grafana
Create a persistent disk to be used for storing Grafana state:
```
gcloud compute disks create grafana --size=50GB --zone=europe-west1-c
```
Create a persistent volume & claim:
```
kubectl create -f pv/grafana.yaml
kubectl create -f pvc/grafana.yaml
```
Create the Grafana deployment:
```
kubectl create -f deployments/grafana.yaml
```
Create the Grafana service:
```
kubectl create -f services/grafana.yaml
```
