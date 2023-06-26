npm install

npm run start

build the image file

docker build . -t explorejava/k8s-web-to-nginx

docker images | grep k8s-web-to-nginx

docker login

docker push explorejava/k8s-web-to-nginx

step 0: minikube start --driver=docker

step 0: minikube status

step 1:
check for existing deployments

$ kubectl get deploy
No resources found in default namespace.

venka@MSI MINGW64 /d/MyProjects/ReactJSApps/k8s/k8s-web-to-nginx
$ kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   109m

step 2:
goto deployment file location run the following command
kubectl apply -f k8s-web-to-nginx.yaml -f nginx.yaml

$ kubectl apply -f k8s-web-to-nginx.yaml -f nginx.yaml
service/k8s-web-to-nginx created
deployment.apps/k8s-web-to-nginx created
service/nginx created
deployment.apps/nginx created

$ kubectl get deploy
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
k8s-web-to-nginx   1/5     5            1           25s
nginx              2/5     5            2           25s

$ kubectl get svc
NAME               TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
k8s-web-to-nginx   LoadBalancer   10.101.19.204    <pending>     3333:30728/TCP   78s
kubernetes         ClusterIP      10.96.0.1        <none>        443/TCP          114m
nginx              ClusterIP      10.109.130.217   <none>        80/TCP           78s


$ kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
k8s-web-to-nginx-79c45dd6b-2pfb6   1/1     Running   0          2m4s
k8s-web-to-nginx-79c45dd6b-fflcf   1/1     Running   0          2m4s
k8s-web-to-nginx-79c45dd6b-jbq7l   1/1     Running   0          2m4s
k8s-web-to-nginx-79c45dd6b-scrx2   1/1     Running   0          2m4s
k8s-web-to-nginx-79c45dd6b-z2x4p   1/1     Running   0          2m4s
nginx-67d4bdd6f5-42xxk             1/1     Running   0          2m4s
nginx-67d4bdd6f5-cbtgn             1/1     Running   0          2m4s
nginx-67d4bdd6f5-gvsh5             1/1     Running   0          2m4s
nginx-67d4bdd6f5-rhfch             1/1     Running   0          2m4s
nginx-67d4bdd6f5-srt7j             1/1     Running   0          2m4s

To run the service

minikube service list

 minikube service k8s-web-to-nginx --alsologtostderr -v=8

$ minikube service k8s-web-to-nginx
🏃  Starting tunnel for service k8s-web-hello.
🎉  Opening service default/k8s-web-hello in default browser...
❗  Because you are using a Docker driver on windows, the terminal needs to be open to run it.



but which is not running

so use port forwarding

$ kubectl port-forward svc/k8s-web-to-nginx 3000:3030
Forwarding from 127.0.0.1:3000 -> 3000
Forwarding from [::1]:3000 -> 3000

step 3:  deleting deployment and service

$ kubectl delete -f k8s-web-to-nginx.yaml -f nginx.yaml
service "k8s-web-to-nginx" deleted
deployment.apps "k8s-web-to-nginx" deleted
service "nginx" deleted
deployment.apps "nginx" deleted


check whether service and deployments exists
$ kubectl get deploy
No resources found in default namespace.

venka@MSI MINGW64 /d/MyProjects/ReactJSApps/k8s
$ kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   72m


minikube dashboard








