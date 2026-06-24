* 신규 서버 추가 후 pod에 이상이 있어 drain 시키는 경우

  kubectl drain k8s-node05 --ignore-daemonsets --delete-emptydir-data

  kubectl get pods -o wide --all-namespaces | grep k8s-node05
