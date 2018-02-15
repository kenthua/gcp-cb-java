# Tool builder: `gcr.io/cloud-builders/mvn`

This Container Builder build step runs Maven. It also includes a number of
dependencies that are precached within the image.

## Building this builder

To build this builder, run the following command in this directory.

    $ gcloud container builds submit . --config=cloudbuild.yaml

* Clone this repo
* Associate it with GC Source Repositories
* Create a build trigger under GC Container Registry
  * Provide a name
  * Trigger Type: `branch`
  * Build configuration: `cloudbuild.yaml`

## Deployment
```
export PROJECT_ID=<YOUR_PROJECT_ID>
```

Replace PROJECT_ID
```
sed -i "s/##PROJECT_ID##/${PROJECT_ID}/g" k8s.yaml
```

Deploy onto your kubernetes instance
``` 
kubectl apply -f k8s.yaml
```

## Force k8s to rollout new image
```
gcloud container images list-tags gcr.io/$PROJECT_ID/spring-boot
```
Copy the short sha tag
```
kubectl set image deployment/sb-hello-world sb-hello-wolrd=gcr.io/$PROJECT_ID/spring-boot:$YOUR_SHORT_SHA_TAG
```

## Cleanup
```
kubectl delete all -l app=sb-hello-world
```