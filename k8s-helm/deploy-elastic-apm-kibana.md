All commands run in kubectl via `ClusterExplorer` in Wrangler

# Install Bitnami Charts

Add bitnami and install elastic:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Install elasticsearch on namespace metals-elastic-dev:

```bash
helm install elasticsearch bitnami/elasticsearch -n metals-elastic-dev
```

This creates a release called `elasticsearch`.

Install kibana:

```bash
helm install -n metals-elastic-dev kibana bitnami/kibana --set elasticsearch.hosts[0]=elasticsearch.metals-elastic-dev.svc.cluster.local,elasticsearch.port=9200,xpack.security.enabled=true,xpack.security.authc.api_key.enabled=true
```

# APM

```bash
# kubectl command line in Wrangler
helm repo add elastic https://helm.elastic.co



```

# Access

Port forward to elastic:

```bash
kubectl port-forward --namespace metals-elastic-dev svc/elasticsearch 9200:9200
kubectl port-forward --namespace metals-elastic-dev svc/apm-server-apm-server 8200:8200
kubectl port-forward --namespace metals-elastic-dev svc/kibana 8080:5601
```

Elasticsearch will be available at `http://localhost:9200`
