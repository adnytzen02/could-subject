# Jenkinsfile 撰寫四個 stage

* '1' podman 
* '2' build image
* '3' push image
* '4' deploy a1


## imagePullSecrets
#### 在主機登入落地 Quay !
    sudo podman login --tls-verify=false mj509.flymks.com:9090 -u mj15r

#### 檢視 auth.json
    sudo cat /run/containers/0/auth.json
{
        "auths": {
                "mj509.flymks.com:9090": {
                        "auth": "cXVheTpRdWF5MTIzNDU="
                }
        }
}

#### 複製 auth.json 到家目錄並變更擁有者
    sudo cp /run/containers/0/auth.json ~
    sudo chown user01:user01 ~/auth.json

#### 建立 K8S Secret
    sudo kubectl create secret generic regcred \
    --from-file=.dockerconfigjson=/home/bigred/auth.json \
    --type=kubernetes.io/dockerconfigjson \
    -n cicd

## Pod 使用 imagePullSecrets 語法
    nano pod-a1.yaml
### pod-a1.ymal
    apiVersion: v1
    kind: Pod
    metadata:
      name: a1
      namespace: cicd
    spec:
      containers:
        - name: a1
          image: mj509.flymks.com:9090/mj15r/alpine.httpd:1.0.0
          imagePullPolicy: Always
      imagePullSecrets:
        - name: regcred

## 先將 Quay 中的 alpine.httpd 設定為 private，手動部署驗證
    sudo kubectl delete pod/a1 -n cicd
    sudo kubectl apply -f pod-a1.yaml
    sudo kubectl get pod -n cicd
### 將 Quay 中的 alpine.httpd 刪除，重新觸發Jenkinsfile !
