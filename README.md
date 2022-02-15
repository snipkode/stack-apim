## GENERATE WSO2AM SERVER APIM TO NEW REPO

Prasyarat Memulai :

- **OKTETO CLI**.
- **Docker Compose**.
- **Kubernetes**

## Tutorial

- Lets get started go to **docs** in order to make your personal namespace by clicking on the following button:

<p align="center">
<a href="https://cloud.okteto.com/deploy">
  <img src="https://okteto.com/develop-okteto.svg" alt="Develop on Okteto">
</a>
</p>

- Clone this repository on **deploy** :

```
  Terminal :
  
  RUN  $ git clone https://github.com/snipkode/stack-apim.git
  RUN  $ git checkout branch master
    
```

- Setup **Working Project Apim** :

```
  Terminal:
  
  RUN $ okteto stack deploy
    
```


- Edit **Dockerfile** ARG :

```
ARG REMOTE_NAME=<YOUR_NEW_REPO_NAME>
ARG MY_EMAIL_GIT=<YOUR_EMAIL>
ARG ACCESS_TOKEN=<YOUR_TOKEN_GITHUB>
```


## 1. KONFIGURASI INGRESS ENDPOINT 

- Ubah subdomain didalam file okteto-stack.yml

```
endpoints:
  <subdomain>:
    - path: /
      service: wso2am
      port: 9443

```

- Contoh perubahan sebagai berikut :

```
endpoints:
  wso2am:
    - path: /
      service: wso2am
      port: 9443

```

```
  gateways
  - path: /
    service: wso2am
    port: 80
```


## 2. KONFIGURASI HOSTNAME

- Ubah hostname pada deployment.toml(production config):

```
[server]
hostname = <host website tanpa https>

```
- Contoh perubahan sebagai berikut :

```
[server]
hostname = "wso2am-snipkode.cloud.okteto.net"

```


## 3. KONFIGURASI ANNOTATION INGRESS K8S MANUAL
 - Tambahkan annotasi **nginx.ingress.kubernetes.io/backend-protocol: HTTPS** disetiap endpoint **https** menggunakan **Lens**

 ```
 annotations:
  nginx.ingress.kubernetes.io/backend-protocol: HTTPS

 ```

- DOKUMENTASI OFFICIAL LINK : https://is.docs.wso2.com/en/latest/setup/changing-the-hostname/
- DEVELOP PRODUCT : https://wso2.github.io/github-repositories.html#IS
- WSDL ADMIN SERVICES : https://is.docs.wso2.com/en/latest/develop/admin-services-for-one-way-operations/


