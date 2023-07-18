# Install `java-web-service` Accelerator

To install this accelerator simply run the following command:
```bash
kubectl apply -f fragments/manifests/fragments.yaml
```
**output**:
```bash
fragment.accelerator.apps.tanzu.vmware.com/enable-live-update-fragment created
fragment.accelerator.apps.tanzu.vmware.com/java-rename-app-fragment created
fragment.accelerator.apps.tanzu.vmware.com/java-rewrite-package-fragment created
fragment.accelerator.apps.tanzu.vmware.com/jvm-version-fragment created
fragment.accelerator.apps.tanzu.vmware.com/readme-override-app-name-fragment created
fragment.accelerator.apps.tanzu.vmware.com/template-catalog-info-fragment created   
fragment.accelerator.apps.tanzu.vmware.com/template-workload-fragment created
accelerator.accelerator.apps.tanzu.vmware.com/java-web-service created
```