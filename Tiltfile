SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", 'guybalmas/<project-name>-source')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')
NAMESPACE = os.getenv("NAMESPACE", default='apps')
OUTPUT_TO_NULL_COMMAND = os.getenv("OUTPUT_TO_NULL_COMMAND", default=' > /dev/null ')

k8s_custom_deploy(
    <project-name>,
    apply_cmd="tanzu apps workload apply -f config/workload.yaml --debug --live-update" +
               " --local-path " + LOCAL_PATH +
               " --source-image " + SOURCE_IMAGE +
               " --namespace " + NAMESPACE +
               " --yes " +
               OUTPUT_TO_NULL_COMMAND +
               " && kubectl get workload <project-name> --namespace " + NAMESPACE + " -o yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    deps=['pom.xml', './target/classes'],
    container_selector='workload',
    live_update=[
      sync('./target/classes', '/workspace/BOOT-INF/classes')
    ],
)
allow_k8s_contexts('<k8s-context>')

k8s_resource(APP_NAME, port_forwards=["8080:8080"],
            extra_pod_selectors=[{'serving.knative.dev/service': APP_NAME}])
