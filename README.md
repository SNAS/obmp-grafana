OpenBMP Grafana Integration
===========================

Grafana can be used with OpenBMP backends to visualize BGP data and statistics.

This repository contains various dashboards that can be used against the 
backends. 

> **Postgres** is preferred right now.


(1) Install Grafana
-------------------
Below is how you can use Grafana via Docker. 

### Install Docker

Install [Docker CE](https://docs.docker.com/install/) per docker instructions. 

### Run Grafana

```docker run``` only needs to be called when first creating the container and when
upgrading the container.  Below is an example of how to install/run the 
container.

```
docker run -d -p 3000:3000 \
    -e "GF_SECURITY_ADMIN_PASSWORD=Snas123" \
    --name grafana -h grafana \
    grafana/grafana:latest
```

> ##### NOTE:
> There are numerous environment variables you can set.  See [Docker Grafana](http://docs.grafana.org/installation/docker/)
> for more details.


(2) Install Grafana Plugins
----------------------------
You will need various plugins.  We recommend installing at least the following:

- Bubble Chart
- Pie Chart
- Datatable Panel
- Status Panel

You can install these as follows:

```
docker exec -it grafana bash
grafana-cli plugins install digrich-bubblechart-panel
grafana-cli plugins install grafana-piechart-panel
grafana-cli plugins install briangann-datatable-panel
grafana-cli plugins install vonage-status-panel
exit
docker restart grafana
```


(3) Add PostgreSQL data source
---------------------------------
Follow the data source [Postgres Install](http://docs.grafana.org/features/datasources/postgres/) 
instructions. 

> #### NOTE:
> A default **user** has been created already, so you can use that.

> **IMPORTANT**
> - By default SSL is enabled for Postgres, but it's using a self-signed cert.

- **username:** openbmp
- **password:** openbmp
- **database:** openbmp
- **host:** If running on the same server, use the public IP or **docker0** 172.17.0.1:5432.
**localhost** will not work. 

(4) Import Dashboards
---------------------

Download to your local machine the dashboards you want to import.

> #### NOTE:
> You do not have to be on the same machine where Grafana is running. You can
> import dashboards from your laptop/desktop via the browser.  

You can get them all using **git**:

```
git clone https://github.com/OpenBMP/obmp-grafana.git
```

Dashbaords will be under ```obmp-grafana/dashboards```

Now you can import them by following the [Grafana Import](http://docs.grafana.org/reference/export_import/#importing-a-dashboard) instructions.    

The **Home** dashboard will need to be updated based on your ```Folders```. 
