```bash
export PROJECT_ID=[...] # Replace `[...]` with the project ID

cat cluster.tf

terraform apply \
    --var project_id=$PROJECT_ID

export KUBECONFIG=$PWD/kubeconfig

gcloud container clusters \
    get-credentials $(terraform output cluster_name) \
    --project $(terraform output project_id) \
        --region $(terraform output region)

kubectl create clusterrolebinding \
    cluster-admin-binding \
    --clusterrole cluster-admin \
    --user $(gcloud config get-value account)

kubectl get nodes

terraform destroy \
    --var project_id=$PROJECT_ID
```
