# pipeline-yamls
基于tekton的pipeline相关文件，结合gitlab、harbor和rancher fleet使用，实现ci/cd持续集成和持续交付

## 查看listen
```
$ kubectl apply -f event-listener.yaml

# 实际上，创建EventListener会生成service
$ kubectl get svc | grep listener
el-hello-listener                ClusterIP   10.102.163.137   <none>        8080/TCP,9000/TCP   25h`
```
## 要在集群外部进行通信，请启用端口转发:
```
$ kubectl port-forward service/el-hello-listener 8080
#kubectl port-forward service/el-hello-listener 8080
#Forwarding from 127.0.0.1:8080 -> 8080
#Forwarding from [::1]:8080 -> 8080
```

## 触发
```
curl -v \
   -H 'content-Type: application/json' \
   -d '{"after": "d138d360aaaac14e9b7a85cb1f9d809925e23211"}' \
   http://localhost:8080
```