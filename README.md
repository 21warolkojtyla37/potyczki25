# Drużyna 25 ZSE Radom

### Misja 0 - kryptonim "Red Tape"
To jest nasza dokumentacja

### Misja 1 - operacja "Otwarte Okno"
Użyliśmy nginxa zainstalowanego graficznie. URLe do usługi:
http://ogloszenia-krytyczne.193.187.69.190.sslip.io:31000/
http://193.187.69.190:31000/

### Misja 2 - kryptonim "Long Horn"
Longhorn jest dostępny w clusterze potyczki w gui. W yamlu przy konfiguracji użyliśmy następujących linijek konfiguracji:
  defaultClass: true
  defaultClassReplicaCount: 1
  defaultReplicaCount: 1

### Misja 3 - operacja "Koci Pazur"
Zainstalowaliśmy graficznie grę tetris na clusterze potyczki.
URL: https://rancher.193.187.67.104.sslip.io/k8s/clusters/c-m-dq646lrx/api/v1/namespaces/default/services/http:tetris:80/proxy/

### Misja 4 - kryptonim "Armor Plate"
Neuvector dostępny w GUI na clusterze potyczki.

### Misja 5 - operacja Czyste Ręce


### Misja 6 - kryptonim Zero Zaufania


### Misja 7 - kryptonim Enigma Reactivation
Na clusterze potyczki
Użyta komenda:

```
kubectl create namespace wywiad
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: deszyfrator
  namespace: wywiad
spec:
  containers:
  - name: deszyfrujacy-kontener
    image: busybox:1.35
    command: 
    - "/bin/sh"
    - "-c"
    - "echo 'Zneutralizowac agenta KREML. Haslo: BURZA_MAJOWA'; exit 0"
  restartPolicy: Never
EOF
```

Wynik:
```
> kubectl get pods -n wywiad 
NAME          READY   STATUS      RESTARTS   AGE
deszyfrator   0/1     Completed   0          14s
> kubectl logs deszyfrator -n wywiad
Zneutralizowac agenta KREML. Haslo: BURZA_MAJOWA
```


### Misja 8 - "For Your Eyes Only"
Na clusterze potyczki

# Tworzenie namespace
kubectl create namespace ogloszenia-krytyczne 2>/dev/null || true

# Część 1: Utworzenie użytkownika "rapid-response-agent"
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: rapid-response-role
  namespace: ogloszenia-krytyczne
rules:
- apiGroups: [""]
  resources: ["pods", "pods/log"]
  verbs: ["get", "list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: rapid-response-binding
  namespace: ogloszenia-krytyczne
subjects:
- kind: User
  name: rapid-response-agent
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: rapid-response-role
  apiGroup: rbac.authorization.k8s.io
EOF

# Część 2: Utworzenie konta serwisowego "automated-response-agent"
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: log-reader
  namespace: ogloszenia-krytyczne
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
- apiGroups: [""]
  resources: ["pods/log"]
  verbs: ["get"]
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: automated-response-agent
  namespace: ogloszenia-krytyczne
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: automated-response-binding
  namespace: ogloszenia-krytyczne
subjects:
- kind: ServiceAccount
  name: automated-response-agent
  namespace: ogloszenia-krytyczne
roleRef:
  kind: Role
  name: log-reader
  apiGroup: rbac.authorization.k8s.io
EOF


### Misja 9 - operacja Slinky Slingshot


### Misja 10 - "Zaginiona Arka"
