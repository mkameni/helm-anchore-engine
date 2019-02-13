### Running Jenkins using helm

#### Demarrage de l'environement minikube :
```shell
  $ minikube start
  $ minikube dashboard
```

#### Creation du namespace :
```shell
  $ kubectl create -f deploy/namespace.yaml
```

#### Deployement (installation) de anchore-engine :
```shell
  $ helm install --name anchoreengine-dev-01 -f helm/values.yaml stable/anchore-engine --namespace anchoreengine-dev-01
  $ kubectl get svc -n anchoreengine-dev-01  anchoreengine-dev-01-anchore-engine-api
```

#### Recuperation du mot de passe admin :
```shell
  $ printf $(kubectl get secret --namespace anchoreengine-dev-01 anchoreengine-dev-01-anchore-engine -o jsonpath="{.data.ANCHORE_ADMIN_PASSWORD}" | base64 --decode); echo
```

#### Suppression de anchore-engine :
```shell
  $ helm delete --purge anchoreengine-dev-01
  $ kubectl delete -f deploy/namespace.yaml
```

Via le dashboard, supprimer egalement le pvc cree
