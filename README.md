Steps followed to test locally built Ambassador image with LightStep Tracing:

- set up local docker registry so that Minikube can pull from it
- build local Ambassador image based on branch
- apply ambassador-rbac-modified.yaml (with image set to local)
- apply ambassador-service.yaml
- apply lightstep-config.yaml (with access token added)
- apply httpbin.yaml
- check set up works so far with `curl <ambassador ip>/httpbin/ip` (should get response)

Testing SaaS:
- apply lightstep-saas-collector.yaml

Testing on-prem:
- apply lightstep-onprem-collector.yaml

Then:
- curl httpbin at `<ambassador ip>/httpbin/` a few times and check LightStep Explorer for spans

See individual yamls for more commentary.