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
# apply
tanzu accelerator apply -f ./fragments/manifests/enable-live-update-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/java-rename-app-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/java-rewrite-package-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/jvm-version-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/template-catalog-info-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/template-workload-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/readme-override-app-name-fragment.yaml

# delete if needed
tanzu accelerator delete -f ./fragments/manifests/enable-live-update-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/java-rename-app-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/java-rewrite-package-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/jvm-version-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/template-catalog-info-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/template-workload-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/readme-override-app-name-fragment.yaml
```

### Reconcile the accelerator 
```bash
tanzu accelerator update my-simple-acc --reconcile
```