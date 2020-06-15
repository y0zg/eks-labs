Ref.: https://aws.amazon.com/blogs/opensource/network-load-balancer-nginx-ingress-controller-eks/

```
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-0.32.0/deploy/static/provider/aws/deploy.yaml

$ kubectl apply -f https://raw.githubusercontent.com/cornellanthony/nlb-nginxIngress-eks/master/apple.yaml

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
    nginx.ingress.kubernetes.io/force-ssl-redirect: "false"
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  tls:
  - hosts:
    - anthonycornell.com
    secretName: tls-secret
  rules:
  - host: anthonycornell.com
    http:
      paths:
        - path: /apple
          backend:
            serviceName: apple-service
            servicePort: 5678
        - path: /banana
          backend:
            serviceName: banana-service
            servicePort: 5678
            
kubectl create -f https://raw.githubusercontent.com/cornellanthony/nlb-nginxIngress-eks/master/example-ingress.yaml

anthonycornell.com.           A.    
ALIAS abf3d14967d6511e9903d12aa583c79b-e3b2965682e9fbde.elb.us-east-1.amazonaws.com 

curl  https://anthonycornell.com/banana -k
Banana

curl  https://anthonycornell.com/apple -k
Apple

apiVersion: extensions/v1beta1
 kind: Ingress
 metadata:
  name: api-ingresse-test
  namespace: test
  annotations:
    kubernetes.io/ingress.class: "nginx"
 spec:
  rules:
  - host: test.anthonycornell.com
    http:
      paths:
      - backend:
          serviceName: myApp
          servicePort: 80
        path: /
```

