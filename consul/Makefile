default: install

PREFIX := consul
TIMEOUT := 1200s
VERSION := 0.39.0
NAMESPACE := $(PREFIX)

install:
	helm repo add hashicorp https://helm.releases.hashicorp.com
	helm repo update
	helm search repo hashicorp/$(PREFIX) --versions

simple:
	helm upgrade --wait --timeout=$(TIMEOUT) --namespace $(NAMESPACE) --create-namespace --install $(PREFIX) hashicorp/$(PREFIX) --values simple.yaml --version $(VERSION)

remove:
	helm --namespace $(NAMESPACE) uninstall $(PREFIX)
