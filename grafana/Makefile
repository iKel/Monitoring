cluster = $(shell basename $$(kubectl config current-context))
version = 1.0
namespace = monitoring

service = grafana
include clusters/$(cluster)/config

# monitoring should run in one namespace
kubectl := kubectl -n $(namespace)
aws := aws --region $(region)


replacements="\
s/NAMESPACE/$(namespace)/g;\
s/SERVICE_NAME/$(service)/g;\
s/HOSTNAME/$(hostname)/g\
"

namespace:
	@cat namespace.yaml | sed $(replacements) | kubectl apply -f -

run: namespace
	@cat configmap.yaml | sed $(replacements) | kubectl apply -f -
	@cat deployment.yaml | sed $(replacements) | kubectl apply -f -
	@cat service.yaml | sed $(replacements) | kubectl apply -f -

stop:
	@cat deployment.yaml | sed $(replacements) | kubectl delete -f - --ignore-not-found
	@cat service.yaml | sed $(replacements) | kubectl delete -f - --ignore-not-found

destroy: stop
	@cat configmap.yaml | sed $(replacements) | kubectl delete -f - --ignore-not-found
