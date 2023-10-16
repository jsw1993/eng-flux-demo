# eng-flux-demo
This is the "GitOps" repo flux looks at and syncs manifests from. The cluster is configured to look in the `clusters/cluster-a` folder and apply manifests from there.

`Bases` contains generic manifests which should be able to be applied to any cluster

`Overlays` contains cluster specific Kustomizations.

The manifests in the clusters folder then reference the kustomization.yaml's in either the bases or overlays folder.

The following services are deployed:
- AWS Load Balancer Controller
- Cert Manager
- Demo Web App [repo here](https://github.com/jsw1993/eng-flux-ci-demo)
- External DNS
- Prometheus Stack
- Terraform Controller

Where IAM is required these are using IAM roles for service accounts.

# If Forking the repo
- You'll need to go through the overlays folder and check/modify any cluster specific Kustomizations
- If you want to use the Terraform Controller as part of Flux you'll need to add a GitHub personal access token with the following: 
`kubectl create secret generic branch-planner-token --namespace=flux-system --from-literal=""`
- **TF Controller is in auto apply mode** this means it will deploy any Terraform in the repo you point it to.

# Other
Yes I'm aware there is a Teams Webhook in here which is not best practice but it's an example used in the demo.