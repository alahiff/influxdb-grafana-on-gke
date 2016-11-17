# InfluxDB & Grafana using Kubernetes on Google Cloud Platform
A simple demonstration of running InfluxDB and Grafana on Google Cloud Platform. Persistent disks are used for both InfluxDB and Grafana. Note that a higher performance disk (e.g. SSD) may be required for InfluxDB for some applications.
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
