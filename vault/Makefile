default: install

PREFIX := vault
TIMEOUT := 1200s
VERSION := 0.18.0
NAMESPACE := $(PREFIX)

install:
	helm repo add hashicorp https://helm.releases.hashicorp.com
	helm repo update
	helm search repo hashicorp/$(PREFIX) --versions

simple:
	helm upgrade --wait --timeout=$(TIMEOUT) --namespace $(NAMESPACE) --create-namespace --install $(PREFIX) hashicorp/$(PREFIX) --values simple.yaml --version $(VERSION)
	kubectl -n $(NAMESPACE) exec -it vault-0 -- vault operator init

autoseal:
	#aws kms create-key | jq '.KeyMetadata.KeyId'
	helm upgrade --wait --timeout=$(TIMEOUT) --namespace $(NAMESPACE) --create-namespace --install $(PREFIX) hashicorp/$(PREFIX) --values autoseal.yaml --version $(VERSION)
	kubectl -n $(NAMESPACE) exec -it vault-0 -- vault operator init

remove:
	helm --namespace $(NAMESPACE) uninstall $(PREFIX)
