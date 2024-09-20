# my-splunk

demo chart to show overriding dependency chart values.

pull chart deps so you can take a look

```bash
helm repo add eformat https://eformat.github.io/helm-charts
helm repo up eformat
helm dep up

$ helm search repo eformat/my-splunk
NAME             	CHART VERSION	APP VERSION	DESCRIPTION
eformat/my-splunk	0.0.1        	0.0.1      	A Helm chart for Kubernetes

```

deploy via argocd

```bash
oc new-project my-splunk
```

`SCC runAsUser` - you will need to set the helm value in `argocd-application.yaml

```yaml
# set this
          containerSecurityContext:
            runAsUser: 1000910000
# from this
$ oc get project my-splunk -o yaml | grep openshift.io/sa.scc.uid-range
    openshift.io/sa.scc.uid-range: 1000910000/10000
```

And apply

```bash
oc apply -f argocd-application.yaml
```
