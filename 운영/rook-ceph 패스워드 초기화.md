* [ rook-ceph 설치 후 패스워드 변경 하지 않음에도 불구하고 admin 계정 초기 패스워드로 접속이 안되는 경우 ]

  1. rook-ceph tools pod 확인 및 접속

    kubectl -n rook-ceph get pods | grep tools

    rook-ceph-tools-657465dd84-k4tbs                   1/1     Running     0             168d
 
    root@avd-k8s2bs01:/sw/helm/values# kubectl -n rook-ceph exec -it rook-ceph-tools-657465dd84-k4tbs -- bash

    bash-4.4$
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  2. admin 계정 활성화 여부 확인 ( enabled: false 상태 )

    bash-4.4$ ceph dashboard ac-user-show admin

    {"username": "admin", "password": "$2b$12$Dc/ENXcXi048gIftkNLPLOr2ag4fZnQO2/dd/y3IhuTB/uKQOYECW", "roles": ["administrator"], "name": null, "email": null, "lastUpdate": 1759196695, "enabled": false, "pwdExpirationDate": null, "pwdUpdateRequired": false}

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  3. admin 계정 활성화 ( enabled: true 상태로 변경 확인 후 로그인 )

    bash-4.4$ ceph dashboard ac-user-enable admin

    {"username": "admin", "password": "$2b$12$Dc/ENXcXi048gIftkNLPLOr2ag4fZnQO2/dd/y3IhuTB/uKQOYECW", "roles": ["administrator"], "name": null, "email": null, "lastUpdate": 1759196795, "enabled": true, "pwdExpirationDate": null, "pwdUpdateRequired": false}
