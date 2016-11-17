# InfluxDB & Grafana using Kubernetes on Google Cloud Platform
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
## Setup Grafana
