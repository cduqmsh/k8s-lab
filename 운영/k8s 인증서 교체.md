- **SSL 인증서 secret 삭제 없이, 갱신은 아래의 명령어 절차로 진행한다**
    
    **1. 신규 인증서 파일이 있는 디렉토리로 이동 (cert.pem 파일 및 key.pem 파일 디렉터리에 업로드)**
    
    cd /home/users/certs/joins.net
    
    **2. 인증서 파일을 encoding하여 임시 저장**
    
    ```bash
    TLS_CRT=$(base64 < "./cert.pem" | tr -d '\n')
    
    TLS_KEY=$(base64 < "./key.pem" | tr -d '\n')
    ```
    
    **3. 인증서 갱신 명령어**
    
    ```bash
    kubectl patch secrets  [Secret Name] -n [secret namespace] -p "{\"data\":{\"tls.key\":\"${TLS_KEY}\",\"tls.crt\":\"${TLS_CRT}\"}}" --type=merge
    ```
    

**4. 인증서 일괄 갱신 가능 여부?**

kubectl patsch 명령어에 flag로 --all-namespace 는 지원되지 않는다. 

namespace를 지정하지 않고, secret 갱신 명령어를 실행하면, secert을 찾지 못한다.

그러므로, 일괄 갱신은 지원이 현재로는 되지 않는다

**5. 인증서 갱신 확인**

```bash
kubectl get secret -n [각 어플리케이션별 namespace]
```

**6.  인증서 갱신 날짜**

```bash
kubectl get secret tls-test.net -n ingress-nginx -o "jsonpath={.data['tls\.crt']}" | base64 -d | openssl x509 -enddate -noout
```
