Steps followed to test locally built ambassador image with LightStep Tracing

Pre-reqs:
- set up local docker registry so that Minikube can pull from it
- build local ambassador image based on branch and push to local registry

Steps:
- `kubectl apply -f ambassador-rbac-modified.yaml` (with image set to local and the right image tag)
- `kubectl apply -f ambassador-service.yaml`
- `kubectl apply -f lightstep-config.yaml` (with access token added in the file)
- `kubectl apply -f httpbin.yaml`
- check set up works so far with `curl <ambassador ip>/httpbin/ip` (should get response)

Testing SaaS:
- `kubectl apply -f lightstep-saas-collector.yaml`

Testing on-prem:
- `kubectl apply -f lightstep-onprem-collector.yaml` (make sure to add your LightStep Satellite API key)

Then:
- restart ambassador (ex. delete the single pod that's running, ambassador needs to be restarted to enable tracing)
- curl httpbin at `<ambassador ip>/httpbin/` a few times and check LightStep Explorer for spans

See individual yamls for more commentary.

Note this is only testing the super happy case. See the Ambassador github for docs on troubleshooting. I troubleshoot(ed? troubleshot?) mostly by enabling ambassador debugging, following along the ambassador pod logs, and adding logging to dump out the envoy configs being generated.
