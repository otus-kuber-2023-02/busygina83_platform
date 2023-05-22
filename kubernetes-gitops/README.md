Все работы проводились в репозитории microservices-demo

inna@HP-Inna:~/otus/kubernetes-gitops/microservices-demo$ kubectl logs helm-operator-6cffbdcc56-ll6tl -n flux | grep frontend
ts=2023-05-22T17:50:59.422231604Z caller=release.go:79 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 info="starting sync run"
ts=2023-05-22T17:50:59.430564386Z caller=release.go:85 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 error="failed to prepare chart for release: could not find valid chart source configuration for release"

Файл .gitlab-ci.yml лежит в корне проекта microservices-demo

Реализуйте установку Istio альтернативным способом: Istio operator
$ kubectl apply -f - <<EOF
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  namespace: istio-system
  name: example-istiocontrolplane
spec:
  profile: default
  values:
    global:
      istioNamespace: microservices-demo
EOF

Ссылка на Ваш инфраструктурный репозиторий:
https://gitlab.com/microservices-demo4/microservices-demo

inna@HP-Inna:~/otus/kubernetes-gitops/microservices-demo$ kubectl get canaries -n microservices-demo
NAME       STATUS        WEIGHT   LASTTRANSITIONTIME
frontend   Initialized   0        2023-05-22T17:20:47Z

inna@HP-Inna:~/otus/kubernetes-gitops/microservices-demo$ kubectl describe canary -n microservices-demo frontend
...
Events:
  Type     Reason  Age                From     Message
  ----     ------  ----               ----     -------
  Warning  Synced  15m                flagger  frontend-primary.microservices-demo not ready: waiting for rollout to finish: observed deployment generation less than desired generation
  Normal   Synced  14m (x2 over 15m)  flagger  all the metrics providers are available!
  Normal   Synced  14m                flagger  Initialization done! frontend.microservices-demo

