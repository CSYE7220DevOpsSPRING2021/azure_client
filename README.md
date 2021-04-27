# azure_client

this is the azure cloud infrastructure, it is used to create azure AKS and deploy the fe container on the same 

# applying the terraform

	terraform init 
	terraform plan <please pass the required variable for the azure cloud>
	terraform applying <please pass the required variable for the azure cloud>
	

# setting up the config file for k8

1. terraform output kube_config > config-terraform-eks-demo

2. cp C:/Users/<username>/.kube/config C:/Users/<username>/.kube/config.bak
3. cp ./config-terraform-eks-demo C:/Users/<username>/.kube/config

# deploying the app

1. kubectl apply -f deployment.yaml 

2. kubectl apply -f uberapp-service_fe.yaml

note- curently in deployment.yaml image is set up as shamsalamnamimi/uber-fe:prod, please change to the new docker immage 

# setting up the monitoring 
	
	kubectl create namespace monitoring

	kubectl apply -f clusterRole.yaml

	kubectl apply -f config-map.yaml	

	kubectl apply -f prometheus-deployment.yaml --namespace=monitoring

	kubectl get deployments --namespace=monitoring


	kubectl get deployments --all-namespaces

	kubectl apply -f prometheus-service.yaml --namespace=monitoring

	kubectl get svc --namespace=monitoring


	kubectl apply -f grafana-datasource-config.yaml

	kubectl apply -f grafana-datasource-deploy.yaml

	kubectl create -f grafana-datasource-service.yaml

	kubectl get svc --namespace=monitoring
