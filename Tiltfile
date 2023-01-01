allow_k8s_contexts('arn:aws:eks:eu-north-1:384617649113:cluster/tap-guy-lab-p8m8nm3rts18')

SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", 'guybalmas/example-k8s-app-source')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')
NAMESPACE = os.getenv("NAMESPACE", default='apps')
OUTPUT_TO_NULL_COMMAND = os.getenv("OUTPUT_TO_NULL_COMMAND", default=' > /dev/null ')
DEFAULT_GREETING_MESSAGE = os.getenv("GREETING_MSG", default='default-greeting-message')
DEFAULT_GREETING_DESCRIPTION = os.getenv("GREETING_DESC", default='default-greeting-description')

k8s_custom_deploy(
    'example-k8s-app',
    apply_cmd="tanzu apps workload apply -f config/workload.yaml --debug --live-update" +
               " --local-path " + LOCAL_PATH +
               " --source-image " + SOURCE_IMAGE +
               " --namespace " + NAMESPACE +
               " --yes " +
               " --env GREETING_MSG=" + DEFAULT_GREETING_MESSAGE + 
               " --env GREETING_DESC=" + DEFAULT_GREETING_DESCRIPTION + 
               OUTPUT_TO_NULL_COMMAND +
               " && kubectl get workload example-k8s-app --namespace " + NAMESPACE + " -o yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    deps=['pom.xml', './target/classes'],
    container_selector='workload',
    live_update=[
      sync('./target/classes', '/workspace/BOOT-INF/classes')
    ],
)


k8s_resource('example-k8s-app', port_forwards=["8080:8080"],
            extra_pod_selectors=[{'serving.knative.dev/service': 'example-k8s-app'}])
