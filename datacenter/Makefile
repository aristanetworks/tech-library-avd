.PHONY: help
help: ## Display help message
	@grep -E '^[0-9a-zA-Z_-]+\.*[0-9a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

.PHONY: build-deploy-cvp-all
build-deploy-cvp-all: ## Ping Nodes
	make build-domain-a build-domain-b build-domain-c build-domain-d build-domain-backbone deploy-cvp-domain-a deploy-cvp-domain-b deploy-cvp-domain-c build-domain-d deploy-cvp-backbone

.PHONY: deploy-cvp-all
deploy-cvp-all: ## Ping Nodes
	make deploy-cvp-domain-a deploy-cvp-domain-b deploy-cvp-domain-c deploy-cvp-domain-d deploy-cvp-backbone

.PHONY: build-all
build-all: ## Ping Nodes
	make build-domain-a build-domain-b build-domain-c build-domain-d build-domain-backbone

########################################################
# Domain A
########################################################

.PHONY: ping-domain-a
ping-domain-a: ## Ping Nodes
	ansible-playbook playbooks/ping.yml -i domain-a/inventory.yml

.PHONY: build-domain-a
build-domain-a: ## Build Configs
	ansible-playbook playbooks/fabric-build.yml --skip-tags documentation -i domain-a/inventory.yml

.PHONY: deploy-eapi-domain-a
deploy-eapi-domain-a: ## Deploy Configs via eAPI
	ansible-playbook playbooks/fabric-deploy-eapi.yml -i domain-a/inventory.yml

.PHONY: deploy-cvp-domain-a
deploy-cvp-domain-a: ## Deploy using CV CI workflow (i.e. workspaces, studios, etc)
	ansible-playbook playbooks/fabric-deploy-cvp.yml -i domain-a/inventory.yml

.PHONY: validate-domain-a
validate-domain-a:
	ansible-playbook playbooks/fabric-validate-state.yml -i domain-a/inventory.yml

########################################################
# Domain B
########################################################

.PHONY: ping-domain-b
ping-domain-b: ## Ping Nodes
	ansible-playbook playbooks/ping.yml -i domain-b/inventory.yml

.PHONY: build-domain-b
build-domain-b: ## Build Configs
	ansible-playbook playbooks/fabric-build.yml --skip-tags documentation -i domain-b/inventory.yml

.PHONY: deploy-eapi-domain-b
deploy-eapi-domain-b: ## Deploy Configs via eAPI
	ansible-playbook playbooks/fabric-deploy-eapi.yml -i domain-b/inventory.yml

.PHONY: deploy-cvp-domain-b
deploy-cvp-domain-b: ## Deploy Configs via CVP
	ansible-playbook playbooks/fabric-deploy-cvp.yml -i domain-b/inventory.yml

.PHONY: validate-domain-b
validate-domain-b:
	ansible-playbook playbooks/fabric-validate-state.yml -i domain-b/inventory.yml

########################################################
# Domain C
########################################################

.PHONY: ping-domain-c
ping-domain-c: ## Ping Nodes
	ansible-playbook playbooks/ping.yml -i domain-c/inventory.yml

.PHONY: build-domain-c
build-domain-c: ## Build Configs
	ansible-playbook playbooks/fabric-build.yml --skip-tags documentation -i domain-c/inventory.yml

.PHONY: deploy-eapi-domain-c
deploy-eapi-domain-c: ## Deploy Configs via eAPI
	ansible-playbook playbooks/fabric-deploy-eapi.yml -i domain-c/inventory.yml

.PHONY: deploy-cvp-domain-c
deploy-cvp-domain-c: ## Deploy using CV CI workflow (i.e. workspaces, studios, etc)
	ansible-playbook playbooks/fabric-deploy-cvp.yml -i domain-c/inventory.yml

.PHONY: validate-domain-c
validate-domain-c:
	ansible-playbook playbooks/fabric-validate-state.yml -i domain-c/inventory.yml

########################################################
# Domain D
########################################################

.PHONY: ping-domain-d
ping-domain-d: ## Ping Nodes
	ansible-playbook playbooks/ping.yml -i domain-d/inventory.yml

.PHONY: build-domain-d
build-domain-d: ## Build Configs
	ansible-playbook playbooks/fabric-build.yml --skip-tags documentation -i domain-d/inventory.yml

.PHONY: deploy-eapi-domain-d
deploy-eapi-domain-d: ## Deploy Configs via eAPI
	ansible-playbook playbooks/fabric-deploy-eapi.yml -i domain-d/inventory.yml

.PHONY: deploy-cvp-domain-d
deploy-cvp-domain-d: ## Deploy using CV CI workflow (i.e. workspaces, studios, etc)
	ansible-playbook playbooks/fabric-deploy-cvp.yml -i domain-d/inventory.yml

.PHONY: deploy-servers-domain-d
deploy-servers-domain-d: ## Deploy Server Configs via eAPI
	ansible-playbook playbooks/server-deploy-eapi.yml -i domain-d/inventory.yml -e "target_hosts=DOMAIN_D_HOSTS"

.PHONY: validate-domain-d
validate-domain-d:
	ansible-playbook playbooks/fabric-validate-state.yml -i domain-d/inventory.yml

########################################################
# BACKBONE
########################################################

.PHONY: ping-backbone
ping-backbone: ## Ping Nodes
	ansible-playbook playbooks/ping.yml -i backbone/inventory.yml

.PHONY: build-domain-backbone
build-domain-backbone: ## Build Configs
	ansible-playbook playbooks/fabric-build.yml --skip-tags documentation -i backbone/inventory.yml

.PHONY: deploy-domain-backbone
deploy-backbone: ## Deploy Configs via eAPI
	ansible-playbook playbooks/fabric-deploy-eapi.yml -i backbone/inventory.yml

.PHONY: deploy-cvp-backbone
deploy-cvp-backbone: ## Deploy using CV CI workflow (i.e. workspaces, studios, etc)
	ansible-playbook playbooks/fabric-deploy-cvp.yml -i backbone/inventory.yml

########################################################
# Servers
########################################################

.PHONY: deploy-servers-eapi
	ansible-playbook playbooks/servers-deploy-eapi.yml -i servers/inventory.yml

.PHONY: deploy-servers-cv
	ansible-playbook playbooks/servers-deploy-cvp.yml -i servers/inventory.yml
	
########################################################
# Replace domain inventory ansible_hosts with ACT inventory ansible_hosts 
########################################################

.PHONY: replace-domain-a-inventory
replace-domain-a-inventory: 
	python3 scripts/convert_inventory-to-act-inventory.py domain-a

.PHONY: replace-domain-b-inventory
replace-domain-b-inventory: 
	python3 scripts/convert_inventory-to-act-inventory.py domain-b

.PHONY: replace-domain-c-inventory
replace-domain-c-inventory: 
	python3 scripts/convert_inventory-to-act-inventory.py domain-c

.PHONY: replace-domain-d-inventory
replace-domain-d-inventory: 
	python3 scripts/convert_inventory-to-act-inventory.py domain-d

.PHONY: replace-backbone-inventory
replace-backbone-inventory: 
	python3 scripts/convert_inventory-to-act-inventory.py backbone
