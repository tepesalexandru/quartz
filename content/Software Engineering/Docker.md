- You need a [[dockerfile]] to build the image of a [[Docker Container|container]]
- Changes to a container do not persist after rebooting it. If you need to persist information across reboots, use [[Volumes|volumes]].
- [[Azure Container Registry]] (ACR) is the place to upload your container images so that later they can be accessed from other services.
- Each [[Docker Image|image]] must be tagged with the following fields:
	- acr_name
	- repository_name
	- version
- The Container Registry is also used for deploying container and can be integrated in [[Azure Pipelines]]
- Login to your registry using `- az acr login --name <acr-name>`
- Tag an image using: 
`docket tag foobar <acr-name>.azurecr.io/<repository-name>/<image-name>`
- Push the image using: 
`docker push <acr-name>.azurecr.io/<repository-name>/<image-name>`
- Create container:
```
az container create 
	--resource-group <rg-name>
	--name <name>
	--image <image-tag>
	--cpu 1
	--memory 1
	...
	auth method
	--ports 80
```
- The [[Azure Container Instance]] (ACI) is used to run the container from the images stored in the ACR.
- Create an image: `docker build --tag=<tag-name>[:version] <dockerfile_dir>`