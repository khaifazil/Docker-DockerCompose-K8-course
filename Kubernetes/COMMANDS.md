# KUBECTL

**CREATE DEPLOYMENT**
`kubectl create deployment --{imageName}
	- image must be in in the pod or from a registry

**DELETE DEPLOYMENT**
`kubectl delete deployment {deploymentName}`
	- command to delete specified service
`kubectl delete -f={path/to/file}, {path/to/second/file}, ...`
	- command to stop and delete declarative deployments

**GET DEPLOYMENTS**
`kubectl get deployment
	- list running deployments

**GET PODS**
`kubectl get pods
	- list running pods

**CREATE/EXPOSE SERVICE**
`kubectl expose deployment {deploymentName} --type={type} --port={portNo.}
	- creates and exposes a service based 
	- --type={typename} - flag to set the type of service
	-  --port={portNo.} - flag to expose the port specified

**GET SERVICES**
`kubectl get services
	- list running services

**DELETE SERVICE**
`kubectl delete service {deploymentName}`
	- command to delete specified service

**SCALING**
`kubectl scale deployment/{deploymentName} --replicas={no.}
	- scales the deployment up to the number of specified replicas
	- --replicas={no. of replicated nodes} - flag to set the type and number of scaling

**UPDATING IMAGES**
`kubectl set image {fileName/TypeName}/{deploymentName} {containerName}={newImageName}`
	- Command to update container's image inside a deployment

**DEPLOYMENT STATUS**
`kubectl rollout status deployment/{deploymentName}`
	- command to check status of deployments

**DEPLOYMENT STATUS**
`kubectl rollout history deployment/{deploymentName}`
	- command to check history of deployments
	- `--revision={revisonNo.}` - flag to check specified deployment revision

**ROLLBACK**
`kubectl rollout undo deployment/{deploymentName}`
	- command to rollback the specified deployment
	- `--to-revision={revisionNo.}` - to roll back to specific deployment revision

# MINIKUBE
**GET EXTERNAL IP ADDRESS**
`minikube service {deploymentName}`
	- command to get the external IP address for the specified deployment

