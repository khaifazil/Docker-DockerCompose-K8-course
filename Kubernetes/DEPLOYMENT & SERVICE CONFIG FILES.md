# What is deployment config used for?
- same as docker-compose
- also known as declarative deployments
- declares all the settings needed for a deployment in one YAML file
- makes it easier to start and stop a deployment

### STARTING A DEPLOYMENT FILE
`kubectl apply -f={path/to/file}`
	- command to run the deployment/service config file
	- `-f={path/to/file}` - required flag to indicate the config file

### STOP/DELETE DEPLOYMENT FILE
`kubectl delete -f={path/to/file},{path/to/second/file},...`
	- command to stop and delete declarative deployments
`kubectl delete {resourseType} -l group={labelName}`
	- command to delete via `-l` label flag
	- have to list the resources to delete, e.g `deployments, services`

### MAKING A CONFIG FILE

```
# Service configurations

apiVersion: v1
kind: Service
metadata:
	name: backend
	labels:
		group: example
spec:
	selector: #exposes pods with labels specified below
		app: second-app
	ports:
		- protocol: 'TCP'
		  port: 80 #port to expose
		  targetPort: 8080 #port inside the container
	  # - protocol: ...
		# port: ...
		# targetPort: ...
	type: LoadBalancer #options 1.ClusterIp 2.NodePort 3.loadBalancer


--- #syntax for merging multiple config files into a single config file
  

# Deployment configurations


apiVersion: apps/v1 #declares which version k8 api to use
kind: Deployment #sets the kind of confiq
metadata:
	name: second-app-deployment #sets the name of the deployment
	labels:
		group: example
spec:
	replicas: 1 #sets the number of pods to start up with
	selector: #selects the pods to control
		matchLabels: #matches template labels
			app: second-app
			tier: backend
	template:
		metadata:
			labels:
				app: second-app
				tier: backend
		spec:
			containers:
				- name: second-node
				  image: muthermutton/kub-first-app:2
				  imagePullPolicy: Always #option to set pull policy on images
				  livenessProbe: #option to configure the health checking of pods
					  httpGet: #reques type
					  path: / #endpoint to check
					  port: 8080 #port to check
					  periodSeconds: 10 #interval to check the health of pods
					  initialDelaySeconds: 5 #inital delay before checking
				  volumeMounts:
					- mountPath: {path/inside/container}
					  name: {volumeName}
				# - name: ...
				  # image: ...
			volumes:
				**refer to adding volumes section
```

### ADDING VOLUMES
**EMPTYDIR**
- Creates a new empty directory and is pod specific
```
volumes:
	- name: story-volume
	  emptyDir: {}
```

**HOSTPATH**
- creates a path shared volume for the pods
```
volumes:
	- name: story-volume
	  hostPath:
		path: /data
		type: DirectoryOrCreate
```

### PERSISTENT VOLUMES

**PERSISTENT VOLUMES CONFIG**
```
apiVersion: v1
kind: PersistentVolume
metadata:
	name: host-pv
spec:
	capacity:
		storage: 1Gi
	volumeMode: Filesystem
	storageClassName: standard
	accessModes:
		- ReadWriteOnce #Read and write permission for pods in a single Node
		# - ReadOnlyMany #Read only permission for m1 or more nodes **does not work with hostPath
		# - ReadWriteMany #Read and write permission for 1 or more nodes **does not work with hostPath
	hostPath:
		path: /data
		type: DirectoryOrCreate
```

PERSISTENT VOLUMES CLAIMS CONFIG
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
	name: host-pvc
spec:
	volumeName: host-pv #Volume name specified in pv.yml
	accessModes:
		- ReadWriteOnce
	storageClassName: standard
	resources:
		requests:
			storage: 1Gi
```

**GET PERSISTENT VOLUMES**
`kubectl get pv`
- command to get all your persistent volumes

**GET PERSISTENT VOLUME CLAIMS**
`kubectl get pvc`
- command to get all your persistent volume claims

### ENV VARIABLES
 To add to Deployment config file
```
spec:
	containers:
		- name: story-node
		  image: muthermutton/story-node-app:2
		  env:
			- name: STORY_FOLDER
			  # value: 'story' #without use of env.yml file
			  valueFrom:
				configMapKeyRef:
					name: data-store-env
					key: folder
		  volumeMounts:
			- mountPath: /app/story
			  name: story-volume
```

env.yml
```
apiVersion: v1
kind: ConfigMap
metadata:
	name: data-store-env
data:
	folder: 'story'
	{key}: {value}
	...
```