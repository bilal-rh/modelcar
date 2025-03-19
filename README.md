# modelcar


1.
Update the model repo value in download_model.py
model_repo = "ibm-granite/granite-3.1-2b-instruct"

2. Build the OCI image
podman build . -t modelcar:latest --platform linux/amd64

3. Push the image to OCI registry
podman push modelcar:latest quay.io/<your-registry>/modelcar:latest

4. Deploy the model. Instead of providing s3 connectcion, selecy URL-v1 and enter the OCI path in the URI
   oci://quay.io/<your-registry>/modelcar:latest


5. Adjust the default timeout in Kserve Inference Service

apiVersion: serving.kserve.io/v1beta1
kind: InferenceService
metadata:
  name: granite-31-2b-instruct
spec:
  predictor:
    annotations:
      **serving.knative.dev/progress-deadline: 30m**