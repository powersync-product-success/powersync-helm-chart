# PowerSync Helm Chart

This Helm chart deploys PowerSync services on a Kubernetes cluster.

## Prerequisites

- Kubernetes 1.16+
- Helm 3.0+
- A MongoDB database

## Installing the Chart

```bash
# Copy the default values and customize them with your MongoDB credentials and other settings
cp values.yaml my-values.yaml
# Edit values.yaml with your specific configuration

# Install the chart with custom values
helm install powersync ./powersync-helm-chart-demo -f my-values.yaml

```

## Configuration

The following table lists the configurable parameters of the PowerSync chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `namespace` | Kubernetes namespace to deploy into | `powersync-poc` |
| `image.repository` | PowerSync image repository | `journeyapps/powersync-service` |
| `image.tag` | PowerSync image tag | `1.4.0` |
| `api.replicas` | Number of API replicas | `2` |
| `powersyncConfig.storage.uri` | MongoDB storage URI | `mongodb+srv://YOUR_BUCKET_STORAGE.mongodb.net` |
| `powersyncConfig.storage.username` | MongoDB storage username | `YOUR_MONGO_DB_USER` |
| `powersyncConfig.storage.password` | MongoDB storage password | `YOUR_PASSWORD` |
| `ingress.host` | Hostname for the ingress | `YOUR_FQDN_HERE.example.com` |

## Security

This chart requires several sensitive configuration values:

1. MongoDB credentials
2. API tokens
3. JWKS keys

It's recommended to use a secure method to manage these secrets, such as:
- Using Helm's `--set-file` option
- Using a secret management tool like Sealed Secrets or Vault
- Using a custom values file that's not committed to version control

## Customizing the Configuration

The PowerSync configuration is fully customizable through the `powersyncConfig` section in your values file. 

## Troubleshooting

1. Check pod logs:
   ```bash
   kubectl logs -n powersync-poc -l app=powersync-RELEASE-NAME-api
   ```

2. Check pod status:
   ```bash
   kubectl get pods -n powersync-poc
   ```# powersync-helm-chart
