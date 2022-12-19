# Custom Cloud Shell Image for Tech Equity Sandbox Project

## Updating the Custom Cloud Shell Image

Steps to update the image locally and from GCP are described below.

### Steps for updating Dockerfile locally
1. After changing the Dockerfile locally, build the Dockerfile. 

```bash
$ docker build -t cloudshell-image .
```

2. Set up docker to authenticate using `gcloud` (only if developer has not previously done this). *Note: Currently only developers with 'Owner' permissions on the stackdriver-sandbox project (where GCR repo is located) can push images to the tech-equity-training-sandbox GCR.*

```bash
$ gcloud auth configure-docker 
```
3. Tag the image. This will enable docker to push it to the correct location (the project GCR registry), and automatically show this image as "latest" unless another tag is specified by adding `:my_tag` to the command below.
```bash
$ docker tag cloudshell-image gcr.io/tech-equity-training-sandbox-2312/cloudshell-image/uncertified
```

4. Finally, push the image. It should be visible in the registry.
```bash
$ docker push gcr.io/tech-equity-training-sandbox-2312/cloudshell-image/uncertified
```

### Steps for updating Dockerfile from GCP

1. If the Dockerfile is available in `tech-equity-training-sandbox` project, edit by running `cloudshell edit Dockerfile` once in the proper directory in Cloud Shell.

2. Build locally and test the image.
```bash
$ cloudshell env build-local # builds the image
$ cloudshell env run # starts the custom environment
$ exit
```
3. Push the image to GCR.
```bash
$ cloudshell env push
```

4. **Don't forget to update the Dockerfile in the GitHub repository to reflect changes.**

More information can be found on the steps above by running `teachme /google/devshell/tutorials/custom-image-tutorial.md` in GCP Cloud Shell.
