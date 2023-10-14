# Monitoring Infrastructure with Prometheus & Grafana

In this example we are monitoring 5 VMS running on Ubuntu 22.04 KVM host that we installed using Vagrant and provisioned using Ansible playbooks.

To make things easier and straightforward we will run our Prometheus and Grafana applications using Docker running on our host machine.

Make sure of course to have Docker installed on your machine. You can follow instructions on installing Docker engine for your machine [here](https://docs.docker.com/get-docker/).

Once you have Docker installed, proceed to the next step.

## Create Docker network

It's a good practice to create a Docker network to allow Prometheus and Grafana containers to communicate with each other. You can create a Docker bridge network like this:

```
docker network create monitoring
```

## Update Prometheus configuration

Open `vm_targets.yml` file and update it with your VMs' IP addresses.

## Run Prometheus Container

```
docker run -d --name prometheus -p 9090:9090 --network monitoring -v ./prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
```

## Run Grafana Container

```
docker run -d --name grafana -p 3000:3000 --network monitoring grafana/grafana
```

## Configure Grafana Dashboard

- Check first that you are able to access your Prometheus web interface at `http://localhost:9090`.
- Check also that your VMs are in `UP` state at `http://localhost:9090/targets`. If they are not, make sure that `node_exporter` is installed and running on your VMs. You can use the command below to check your `node_exporter`'s status in your VMs.
  ```
  sudo systemctl status node_exporter
  ```
- If everything above is set up correctly, access Grafana's web interface at `http://localhost:3000`

## Import data sources into Grafana

We have to import our VMs data from Prometheus into Grafana in order to create visualizations around it.
