**TP1 Kubernetes**

1. Installer Minikube et Kubectl 
- Minikube :

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
![](https://i.imgur.com/C6U4Rmp.png)

- Kubectl : 
```
minikube kubectl -- get po -A
```
![](https://i.imgur.com/HWG55QA.png)




**Pod Nginx** 

a. Héberger un premier Pod Nginx

*déployer un pod nginx :*

`kubectl run my-pod-nginx --image=nginx`




*Le résultat qu'on obtient est :*
```
 kubectl run my-pod-nginx --image=nginx

pod/my-pod-nginx created
```



b. A l’aide de la commande kubectl port-forward et d’un navigateur accéder à la page par défaut de votre pod Nginx 
    
`kubectl port-forward my-pod-nginx 80:8080`

Le résultat : 
```
kubectl port-forward my-pod-nginx 8080:8080

Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

 
**Connexion entre plusieurs Pods**        

a. A l’image du TP 1 sur Docker (question 7 et 8), héberger un Pod phpmyadmin et mysql, cette fois-ci en utilisant minikube
        
- Mysql        

Fichier de configuration Mysql

![](https://i.imgur.com/pvyw68M.png)

Application de la config

```
kubectl apply -f config_mysql.yml 

deployment.apps/mysql configured
service/mysql unchanged
```

- PhpMyAdmin
        
Fichier de configuration PhpMyAdmin

![](https://i.imgur.com/fcBIQZr.png)


Application de la config

```
kubectl apply -f config_phpmyadmin.yml

deployment.apps/phpmyadmin-deployment created
service/phpmyadmin-service created
```



b. Créer un service associé au Pod mysql

On a nos 2 fichiers de config : 
- Fichier Mysql
- Fichier PhpMyAdmin

Le service associé au pod Mysql est : 

![](https://i.imgur.com/6rKPD8C.png)


c. Connecter phpmyadmin avec le Service mysql et vérifier que vous pouvez administrer cette base de données 

Pour connecter PhpMyAdmin avec le service Mysql, on exécute : 

![](https://i.imgur.com/l43QBbI.png)

On applique la commande : 

```
kubectl apply -f config_phpmyadmin.yml
```


d. Avec la commande kubectl-port forward, vérifier que phpmyadmin arrive à contacter et administrer votre base de données mysql 

```
kubectl port-forward phpmyadmin-deployment 8080:80

Forwarding from 127.0.0.1:8080 -> 80
Forwarding from [::1]:8080 -> 80

Handling connection for 8080
Handling connection for 8080
Handling connection for 8080
```

![](https://i.imgur.com/AbNtIbJ.png)


e. Ajouter un Ingress pour accéder à phpmyadmin sans utiliser la commande kubectl port-forward

![](https://i.imgur.com/16fILIb.png)

On applique la commande : 

`kubectl apply -f ingress phpmyadmin.yml`

