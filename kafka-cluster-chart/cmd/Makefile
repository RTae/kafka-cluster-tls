SHELL := /usr/bin/env bash

help:
	@echo ""
	@echo "Usage: make [TARGET] [OPTIONAL_ARGUMENTS]"
	@echo ""
	@echo "Where:"
	@echo "  cluster=<cluster_name>         clustername"
	@echo "  user=<username>                username"
	@echo "  password=<password>            password"
	@echo "" 
	@echo "example"
	@echo "Usage: make create-secret cluster=datalake-k8s-staging user=user password=password"
	@echo "Usage: make create-secret cluster=datalake-k8s-prod user=user password=password"

create-secret:
	mkdir -p  $(user)

	## generate file in local: ca.crt
	kubectl get secret $(cluster)-cluster-ca-cert -n kafka -o jsonpath='{.data.ca\.crt}' | base64 --decode > $(user)/ca.crt

	keytool -keystore $(user)/truststore.jks -storepass $(password) -alias CARoot -import -file $(user)/ca.crt -noprompt

	## generate file in local: user.crt, user.key, user.p12
	kubectl get secret $(user) -n kafka -o yaml -o jsonpath='{.data.user\.crt}' | base64 --decode > $(user)/user.crt 
	kubectl get secret $(user) -n kafka -o yaml -o jsonpath='{.data.user\.key}' | base64 --decode > $(user)/user.key
	openssl pkcs12 -export -in $(user)/user.crt -inkey $(user)/user.key  -password pass:$(password) -out $(user)/keystore.p12

	## create k8s secret as truststore keystore
	kubectl create secret generic $(user)-auth-tls \
					  --from-file=$(user)/truststore.jks \
					  --from-file=$(user)/keystore.p12 \
					  --from-literal=password=$(password) \
					  -n kafka

	@echo "Cluser name: $(cluster)" 
	@echo "Username: $(user)"
	@echo "Secret name which store certificate: $(user)-auth-tls"

	##  generate file in local: pass
	echo $(password) > $(user)/pass
