# <span style="color: lightblue;">Prometheus<img src="https://prometheus.io/assets/prometheus_logo_grey.svg" alt="promethius" width="30px" height="30px"> and Grafana<img src="https://styles.redditmedia.com/t5_39cr8/styles/communityIcon_fs476g5i1i521.jpg" alt="promethius" width="30px" height="30px"> Setup.</span>
This repository provides Makefiles for easy setup and configuration of Prometheus and Grafana for monitoring your applications on Kubernetes. Prometheus is an open-source monitoring and alerting system, while Grafana is a visualization and dashboarding tool.

___
### <span style="color: teal;">Customize Configuration</span>
The provided Makefiles and YAML files are basic configurations to get you started. You can customize these files (e.g., adjust storage sizes, retention periods) to suit your specific monitoring needs.

**Note:**
* using namspace - "monitoring" for both prometheus and grafana
* specify your cluster name to pick up config file (promethius/cluisters/<span style="color: #994444;">**"yourcluster'**</span>/config - same for grafana)
___

### <span style="color: teal ;">Prerequisites</span>
Kubernetes: You should have a working Kubernetes cluster, and kubectl configured to communicate with it.
___

## Set Up Prometheus:
Use the following command to set up Prometheus and related components in the monitoring namespace:

    make run
<details>
  <summary>This command will deploy:</summary>
  
* Prometheus server 
* kube-state-metrics
* node-exporter
* and other necessary resources for monitoring.
</details>

___


## Access Prometheus UI:
To access the Prometheus UI, forward the Prometheus server port to your local machine using the following command:

    make forward

Now, open your web browser and navigate to http://localhost:9090 to access the Prometheus web interface.

---

## Stopping and Cleaning Up
To stop and clean up the Prometheus

    make stop       # Stop Prometheus services
    make clean      # Delete Prometheus and Grafana resources, but keep PVC 
    make destroy    # Completely remove Prometheus including PVC
---

## Set Up Grafana:
Use the following command to set up Grafana and related components in the monitoring namespace:

    make run
---
Now, open your web browser and navigate to http://localhost:3000 to access the Grafana web interface. Use the default login credentials (admin/admin), and change the password after the first login.

## Import Grafana Dashboards:
If you have specific Grafana dashboards you'd like to use, you can import them to visualize various metrics. Some useful dashboards are available at Grafana's official dashboard repository: https://grafana.com/grafana/dashboards
___
Stopping and Cleaning Up
To stop and clean up the Prometheus and Grafana resources, use the following commands:

    make stop       # Stop Grafana services
    make destroy    # Completely remove Grafana resources, including configuration
___
## Acknowledgments
Prometheus: https://prometheus.io/

Grafana: https://grafana.com/