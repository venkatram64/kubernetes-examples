npm install

npm run start

docker build . -t explorejava/k8s-web-hello

docker images | grep k8s-web-hello

docker login

docker push explorejava/k8s-web-hello

step 1:
goto deployment file location run the following command
kubectl apply -f deployment.yaml

$ kubectl apply -f deployment.yaml
deployment.apps/k8s-web-hello created

$ kubectl get deploy
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
k8s-web-hello   1/1 

$ kubectl get pods
NAME                             READY   STATUS    RESTARTS   AGE
k8s-web-hello-56bc84bfcb-jx6rs   1/1     Running   0          2m5s
venka@MSI MINGW64 /d/MyProjects/ReactJSApps/k8s


$ kubectl get deploy
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
k8s-web-hello   5/5     5            5           7m17s


$ kubectl get pods
NAME                             READY   STATUS    RESTARTS   AGE
k8s-web-hello-56bc84bfcb-7wfmn   1/1     Running   0          23s
k8s-web-hello-56bc84bfcb-8dgdz   1/1     Running   0          23s
k8s-web-hello-56bc84bfcb-gxbw8   1/1     Running   0          23s
k8s-web-hello-56bc84bfcb-jx6rs   1/1     Running   0          6m16s
k8s-web-hello-56bc84bfcb-lp88g   1/1     Running   0          23s


$ kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   59m


step 2:

$ kubectl apply -f service.yaml 
service/k8s-web-hello created

$ kubectl get svc
NAME            TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
k8s-web-hello   LoadBalancer   10.96.72.98   <pending>     3030:30982/TCP   21s
kubernetes      ClusterIP      10.96.0.1     <none>        443/TCP          64m

To run the service

$ minikube service k8s-web-hello
🏃  Starting tunnel for service k8s-web-hello.
🎉  Opening service default/k8s-web-hello in default browser...
❗  Because you are using a Docker driver on windows, the terminal needs to be open to run it.



but which is not running

so use port forwarding

$ kubectl port-forward svc/k8s-web-hello 3000:3030
Forwarding from 127.0.0.1:3000 -> 3000
Forwarding from [::1]:3000 -> 3000

step 3:  deleting deployment and service

$ kubectl delete -f deployment.yaml -f service.yaml
deployment.apps "k8s-web-hello" deleted
service "k8s-web-hello" deleted


check whether service and deployments exists
$ kubectl get deploy
No resources found in default namespace.

venka@MSI MINGW64 /d/MyProjects/ReactJSApps/k8s
$ kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   72m








