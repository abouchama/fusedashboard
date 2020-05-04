The following Grafana resources are supported:

- Grafana
- GrafanaDashboard
- GrafanaDatasource

all custom resources use the api group `integreatly.org` and version `v1alpha1`.

# Creating Grafana Instance

$ oc create -f grafana.yaml

# Creating Grafana Datasource

$ oc create -f prometheus-ds.yaml

# Creating Fuse dashboard

By default the operator only watches for dashboards in it's own namespace. To watch for dashboards in other namespaces, the `--scan-all` flag must be passed.

To create Fuse Dashboard in the fuse namespace run:

$ oc create -f FuseDashboard.yaml -n fuse

NOTE: it can take up to a minute until new dashboards are discovered by Grafana.
