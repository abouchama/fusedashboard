The Grafana operator provides the following api resources:

- Grafana
- GrafanaDashboard
- GrafanaDatasource

all custom resources use the api group `integreatly.org` and version `v1alpha1`.

# Install Grafana Operator

```
cat <<EOF | kubectl apply -f -
apiVersion: operators.coreos.com/v1alpha1
kind: Subscription
metadata:
  name: grafana-operator
  namespace: fuse7
spec:
  channel: alpha
  installPlanApproval: Automatic
  name: grafana-operator
  source: community-operators
  sourceNamespace: openshift-marketplace
EOF
```

Since the operator takes some time to install, We should wait for it to complete.
We can check with if the `status` is `Succeeded` with the following command:

```
oc get csv -n fuse7 grafana-operator.v2.0.0 -o jsonpath='{.status.phase}'
```

# Creating Grafana Instance
```
$ oc create -f https://raw.githubusercontent.com/abouchama/fusedashboard/master/grafana.yaml
```

Open Grafana Console:

```
open https://$(oc get routes/grafana-route -o yaml | yq read - 'spec.host')
```

# Creating Grafana Datasource
```
$ oc create -f https://raw.githubusercontent.com/abouchama/fusedashboard/master/prometheus-ds.yaml
```
# Creating Fuse dashboard

By default the operator only watches for dashboards in it's own namespace. To watch for dashboards in other namespaces, the `--scan-all` flag must be passed.

To create Fuse Dashboard in the fuse namespace run:
```
$ oc create -f https://raw.githubusercontent.com/abouchama/fusedashboard/master/FuseDashboard.yaml
```
NOTE: it can take up to a minute until new dashboards are discovered by Grafana.
