# Sciebo RDS Helm Charts

This repo holds all charts for the sciebo rds microservices.

## Usage

Add this charts to your repository list.

```bash
helm repo add sciebo-rds https://sciebo-rds.github.io/charts/
```

Verify that the repo finds the charts

```bash
helm search repo sciebo-rds
```

## Install the whole system

If you want to install the whole system, you can use the *all* chart, which depends on all services. You have to specify a values.yaml file to set all required parameters.

The following commands will add the needed repository, add a values.yaml file and opens it with vi. After you enter your credentials, it will try to install the chart with all services under the name "sciebo-rds" in your configured cluster.

```bash
helm repo add sciebo-rds https://sciebo-rds.github.io/charts/
cat > values.yaml <<EOF
circle1-port-zenodo:
  environment: 
    ZENODO_ADDRESS: https://sandbox.zenodo.org
    ZENODO_OAUTH_CLIENT_ID: ""
    ZENODO_OAUTH_CLIENT_SECRET: ""
circle1-port-owncloud:
  environment:
    OWNCLOUD_INSTALLATION_URL: https://localhost/owncloud
    OWNCLOUD_OAUTH_CLIENT_ID: ""
    OWNCLOUD_OAUTH_CLIENT_SECRET: ""
EOF
vi values.yaml
helm upgrade sciebo-rds sciebo-rds/all --install --values values.yaml
```

The following table lists the most used configurable parameters of the Sciebo RDS chart and their default values.

| Parameter                                                       | Description | Default                    |
| --------------------------------------------------------------- | ----------- | -------------------------- |
| circle1-port-zenodo.environment.ZENODO_ADDRESS                  |             | https://sandbox.zenodo.org |
| circle1-port-zenodo.environment.ZENODO_OAUTH_CLIENT_ID:         | Required    |                            |
| circle1-port-zenodo.environment.ZENODO_OAUTH_CLIENT_SECRET:     | Required    |                            |
| circle1-port-owncloud.environment.OWNCLOUD_INSTALLATION_URL:    |             | https://localhost/owncloud |
| circle1-port-owncloud.environment.OWNCLOUD_OAUTH_CLIENT_ID:     | Required    |                            |
| circle1-port-owncloud.environment.OWNCLOUD_OAUTH_CLIENT_SECRET: | Required    |                            |

If you need more parameters, please take a look into the values.yaml of the corresponding service.

### Dependencies

This chart also use [jaeger](https://github.com/jaegertracing/helm-charts) and [redis-ha](https://github.com/DandyDeveloper/charts/tree/master/charts/redis-ha). Take a look to the corresponding repositories to find all options.