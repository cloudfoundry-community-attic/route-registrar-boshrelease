# Deploy route-registrar using BOSH

Continuously broadcast a route using NATS to the CF router.

Colocate the `route-registrar` job template with any process that wants to have an HTTP hostname routed to it via the Cloud Foundry router.

Usage
-----

There is an standalone manifest that you can use to advertise another `hostname:port` as a route.

```
git clone https://github.com/cloudfoundry-community/route-registrar-boshrelease.git
cd route-registrar-boshrelease
bosh2 deploy manifests/route-registrar.yml \
  -v route-registrar-external-host=... \
  -v route-registrar-external-ip=... \
  -v route-registrar-port=... \
  -v nats-host=... \
  -v nats-username=... \
  -v nats-password=... \
  -v route-registrar-health-check-name=...
```

But typically you will collocate the `route-registrar` job on the instance group running the `hostname:port` being advertised.
