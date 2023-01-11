# Tanzu Java Web Application Accelerator

This accelerator generates Java web application projects, configured for `Tanzu Application Platform`.

## Features:
1. Supports Unit-Testing using `TAP`'s OOTB `source-test-scan-to-url` supply chain.
2. Supports automatic API registeration in `API Catalog` for application's runtime generated API. 
3. Supports templating catalog-info for application regitration in `Service Catalog` including listing provided API's.  
4. Optional: Supports live-update and live-debug.
5. Optional: Supports cluster choice (local only, all contexts or custom cluster context). 

---

## Apply Fragments onto `TAP`

### List currently installed fragments
```bash
tanzu accelerator fragment list
```

### Create a YAML manifest for the fragment
```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Fragment
metadata:
  name: <fragment-name>
  namespace: accelerator-system
spec:
  displayName: <display-name>
  git:
    ref:
      branch: <branch>
    url: https://github.com/GuyBalmas/tanzu-application-accelerator.git
    subPath: fragments/<fragment-folder>
```

### Apply
```bash
tanzu accelerator apply -f <YAML-file-path>

# apply this accelerator's fragments 
tanzu accelerator apply -f ./fragments/manifests/enable-live-update-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/java-rename-app-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/java-rewrite-package-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/jvm-version-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/template-catalog-info-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/template-workload-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/readme-override-app-name-fragment.yaml

# delete if needed
tanzu accelerator delete -f <YAML-file-path>
# or
tanzu accelerator fragment delete <fragment-name>
```

## Apply Accelerator onto `TAP`

### Create a YAML manifest for the Accelerator
```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Accelerator
metadata:
  name: <accelerator-name>
  namespace: accelerator-system
spec:
  git:
    url: <git-repo-url>
    ref:
      branch: <git-branch>
```

### Apply

```bash
kubectl apply -f <accelerator-manifest-path>

# for example
kubectl apply -f fragments/manifests/accelerator-manifest.yaml
```

### Reconcile the accelerator 
```bash
tanzu accelerator update my-simple-acc --reconcile
```