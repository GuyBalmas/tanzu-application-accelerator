allow_k8s_contexts('arn:aws:eks:eu-north-1:384617649113:cluster/tap-guy-lab-p8m8nm3rts18')

APP_NAME = os.getenv("APP_NAME", 'example-java-app')
SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", 'guybalmas/' + APP_NAME + '-source')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')
NAMESPACE = os.getenv("NAMESPACE", default='apps')
OUTPUT_TO_NULL_COMMAND = os.getenv("OUTPUT_TO_NULL_COMMAND", default=' > /dev/null ')

k8s_custom_deploy(
    APP_NAME,
    apply_cmd="tanzu apps workload apply -f config/workload.yaml --debug --live-update" +
               " --local-path " + LOCAL_PATH +
               " --source-image " + SOURCE_IMAGE +
               " --namespace " + NAMESPACE +
               " --yes " +
               OUTPUT_TO_NULL_COMMAND +
               " && kubectl get workload " + APP_NAME + " --namespace " + NAMESPACE + " -o yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    deps=['pom.xml', './target/classes'],
    container_selector='workload',
    live_update=[
      sync('./target/classes', '/workspace/BOOT-INF/classes')
    ],
)

k8s_resource(APP_NAME, port_forwards=["8080:8080"],
            extra_pod_selectors=[{'serving.knative.dev/service': APP_NAME}])
