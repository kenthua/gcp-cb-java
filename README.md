# Tool builder: `gcr.io/cloud-builders/mvn`

This Container Builder build step runs Maven. It also includes a number of
dependencies that are precached within the image.

## Building this builder

To build this builder, run the following command in this directory.

    $ gcloud container builds submit . --config=cloudbuild.yaml


## Force k8s to rollout new image, since it's only tagged latest
```
kubectl set image deployment/testjava testjava=gcr.io/$PROJECT_ID/spring-boot:latest
```