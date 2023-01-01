# tanzu-application-accelerator

```bash
export GIT_REPOSITORY_URL=https://github.com/GuyBalmas/tanzu-application-accelerator.git
export GIT_BRANCH=main
export ACCELERATOR_NAME=my-simple-acc
```

```bash
tanzu accelerator create ${ACCELERATOR_NAME} --git-repository ${GIT_REPOSITORY_URL} --git-branch ${GIT_BRANCH}
```
**output:**
```bash
created accelerator my-simple-acc in namespace accelerator-system
```

### Updating an accelerator
After you push any changes to your Git repository, the accelerator is refreshed based on the git.interval setting for the Accelerator resource. The default value is 10 minutes. To force an immediate reconciliation, run:
```bash
tanzu accelerator update ${ACCELERATOR-NAME} --reconcile
```

### Deleting an accelerator
```bash
tanzu accelerator delete ACCELERATOR-NAME
```

### Using an accelerator manifest
You can also create a separate manifest file and apply it to the cluster by using the Tanzu CLI:

1. Create a simple-manifest.yaml file and add the following content:
```bash
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Accelerator
metadata:
  name: simple
  namespace: accelerator-system
spec:
  git:
    url: YOUR-GIT-REPOSITORY-URL
    ref:
      branch: YOUR-GIT-BRANCH
```
2. Apply:
```bash
kubectl apply -f simple-manifest.yaml
```
