# gsp304

1. Build a tagged Docker Image
  ```
  gsutil cp gs://[PROEJCT_ID]/resources-echo-web.tar.gz .
  tar zxf resources-echo-web.tar.gz
  export PROJECT_ID="$(gcloud config get-value project -q)"
  docker build -t gcr.io/${PROJECT_ID}/echo-app:v1 .
  ```
2. Push the image to the Google Container Registry
  ```
  gcloud docker -- push gcr.io/${PROJECT_ID}/echo-app:v1
  ```
3. Create a Kubernetes Cluster
  ```
  gcloud container clusters create echo-cluster \
  --machine-type=n1-standard-2 \
  --num-nodes=1 \
  --zone us-central1-a \
  --node-locations us-central1-a,us-central1-b
  ```
4. Deploy the application to the Kubernetes Cluster
  ```
  source <(kubectl completion bash)
  gcloud container clusters get-credentials echo-cluster --zone us-central1-a
  ```
  ```
  kubectl apply -f echo-web.yaml
  kubectl apply -f echo-service.yaml
  ```
  ```
  kubectl get pods
  kubectl get deployments
  kubectl get services
  ```
