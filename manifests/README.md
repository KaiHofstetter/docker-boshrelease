# Deployment

There are two basic use cases supported by the Docker BOSH release:

* statically configure and run one or more containers
* service broker to allow dynamic provisioning of containers

## Static containers

```
bosh2 int manifests/containers-example.yml
```

## Brokered containers

```
bosh2 deploy manifests/broker-containers.yml --vars-store=tmp/creds.yml \
  -o manifests/brokered-services/mysql56.yml \
  -o manifests/brokered-services/redis28.yml
```

See `manifests/brokered-services/*.yml` for example service catalogs you can include in your service broker deployment.

Once deployed, you can dynamically provision new Docker containers using the Service Broker API.

### Integration with Cloud Foundry

You can also integrate your service broker with your Cloud Foundry.

```
bosh2 deploy manifests/broker-containers.yml --vars-store=tmp/creds.yml \
  -o manifests/brokered-services/mysql56.yml \
  -o manifests/brokered-services/redis28.yml \
  -o manifests/op-cf-integration.yml

bosh2 run-errand broker-registrar
```

Each of your services will be now available in the service catalog/marketplace:

```
cf marketplace
```