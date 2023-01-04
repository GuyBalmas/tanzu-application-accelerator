```bash
tanzu accelerator fragment list
```

```yaml
apiVersion: accelerator.apps.tanzu.vmware.com/v1alpha1
kind: Fragment
metadata:
  name: java-version
  namespace: accelerator-system
spec:
  displayName: Select Java Version
  git:
    ref:
      tag: tap-1.3
    url: https://github.com/vmware-tanzu/application-accelerator-samples.git
    subPath: fragments/java-version
```

apply
```bash
tanzu accelerator apply -f ./java-version.yaml

tanzu accelerator apply -f ./fragments/manifests/enable-live-update-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/java-rename-app-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/java-rewrite-package-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/jvm-version-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/template-catalog-info-fragment.yaml
tanzu accelerator apply -f ./fragments/manifests/template-workload-fragment.yaml

tanzu accelerator delete -f ./fragments/manifests/enable-live-update-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/java-rename-app-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/java-rewrite-package-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/jvm-version-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/template-catalog-info-fragment.yaml
tanzu accelerator delete -f ./fragments/manifests/template-workload-fragment.yaml

```

tanzu accelerator update my-simple-acc --reconcile