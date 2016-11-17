# InfluxDB & Grafana using Kubernetes on Google Cloud Platform
Create a persistent disk to be used as the storage for InfluxDB:
```
gcloud compute disks create influxdb --size=200GB --zone=europe-west1-c
```
Create a persistent volume for InfluxDB:
```
kubectl create -f pv/influxdb.yaml
```
Create a persistent volume claim for InfluxDB:
```
kubectl create -f pvc/influxdb.yaml
```
