# Домашнее задание к занятию «Базовые объекты K8S»

### Цель задания

В тестовой среде для работы с Kubernetes, установленной в предыдущем ДЗ, необходимо развернуть Pod с приложением и подключиться к нему со своего локального компьютера. 

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключенным Git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Описание [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) и примеры манифестов.
2. Описание [Service](https://kubernetes.io/docs/concepts/services-networking/service/).

------

### Задание 1. Создать Pod с именем hello-world

1. Создать манифест (yaml-конфигурацию) Pod.
2. Использовать image - gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
3. Подключиться локально к Pod с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

nano pod.yaml

![alt text](https://github.com/MaratKN/kuber-homeworks-02/blob/main/1.png)

kubectl apply -f pod.yaml

kubectl get pods -o wide

![alt text](https://github.com/MaratKN/kuber-homeworks-02/blob/main/2.png)

kubectl port-forward pods/kmn 8080

![alt text](https://github.com/MaratKN/kuber-homeworks-02/blob/main/3_v2.png)

------

### Задание 2. Создать Service и подключить его к Pod

1. Создать Pod с именем netology-web.
2. Использовать image — gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
3. Создать Service с именем netology-svc и подключить к netology-web.
4. Подключиться локально к Service с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

root@DebianNew:~/.kube# nano netology-web.yaml

![alt text](https://github.com/MaratKN/kuber-homeworks-02/blob/main/4.png)


root@DebianNew:~/.kube# kubectl apply -f netology-web.yaml

pod/netology-web created

root@DebianNew:~/.kube# kubectl get pods -o wide
```
NAME           READY   STATUS    RESTARTS   AGE   IP             NODE        NOMINATED NODE   READINESS GATES
kmn            1/1     Running   1          31m   192.168.40.3   debiannew   <none>           <none>
netology-web   1/1     Running   0          5s    192.168.40.8   debiannew   <none>           <none>
```

root@DebianNew:~/.kube# nano netology-svc.yaml

![alt text](https://github.com/MaratKN/kuber-homeworks-02/blob/main/5.png)

root@DebianNew:~/.kube# kubectl apply -f netology-svc.yaml 

service/netology-svc created

![alt text](https://github.com/MaratKN/kuber-homeworks-02/blob/main/6.png)

root@DebianNew:~/.kube# kubectl get svc -o wide
```
NAME           TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE    SELECTOR
kubernetes     ClusterIP   10.152.183.1     <none>        443/TCP    2d9h   <none>
netology-svc   ClusterIP   10.152.183.242   <none>        8080/TCP   39s    app=netology
```

root@DebianNew:~/.kube# kubectl port-forward services/netology-svc 8081:8080

![alt text](https://github.com/MaratKN/kuber-homeworks-02/blob/main/7.png)



------

### Правила приёма работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода команд `kubectl get pods`, а также скриншот результата подключения.
3. Репозиторий должен содержать файлы манифестов и ссылки на них в файле README.md.

------

### Критерии оценки
Зачёт — выполнены все задания, ответы даны в развернутой форме, приложены соответствующие скриншоты и файлы проекта, в выполненных заданиях нет противоречий и нарушения логики.

На доработку — задание выполнено частично или не выполнено, в логике выполнения заданий есть противоречия, существенные недостатки.
