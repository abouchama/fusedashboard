# Creating Grafana Data Source



# Creating Fuse dashboard
By default the operator only watches for dashboards in it's own namespace. To watch for dashboards in other namespaces, the --scan-all flag must be passed.

To create Fuse Dashboard in the fuse namespace run:

$ kubectl create -f FuseDashboard.yaml -n fuse

NOTE: it can take up to a minute until new dashboards are discovered by Grafana.
