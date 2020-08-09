

## Prepare docker images

    # 1 Ansible Controller
    cd /path/to/docker/cicd-local-dev/ansible/centos7/
    docker build -t ansible_controller:0.1 .

    # 2 Jenkins Master test machine blank image
    cd /path/to/docker/cicd-local-dev/jenkins-master/
    docker build -t jenkins-master:blank .

## Run local env

    $ cd /path/to/docker/cicd-local-dev/k8s/

    $ kubectl apply -f  local-dev.yaml

    $ kubectl exec -it $(kubectl get pods --selector=app=ansible-pod -o jsonpath='{.items[*].metadata.name}') -- /bin/bash

    $ kubectl exec -it $(kubectl get pods --selector=app=jenkins-pod -o jsonpath='{.items[*].metadata.name}') -- /bin/bash


    ## Tips
    $ kubectl get pods --show-labels
    ---
    NAME                       READY   STATUS    RESTARTS   AGE   LABELS
    ansible-689f5cdfc5-mbp6l   1/1     Running   0          26m   app=ansible-pod,pod-template-hash=689f5cdfc5
    jenkins-675b975d98-7hkl7   1/1     Running   0          48s   app=jenkins-pod,pod-template-hash=675b975d98
    ---

    $ kubectl get -f local-dev.yaml
    ---
    NAME      READY   UP-TO-DATE   AVAILABLE   AGE
    ansible   1/1     1            1           11m
    jenkins   1/1     1            1           75s
    ---

    $ kubectl get deployment ansible
    ---
    NAME      READY   UP-TO-DATE   AVAILABLE   AGE
    ansible   1/1     1            1           11m
    ---


    ## If you want to delete
    kubectl delete -f local-dev.yaml


## Communication between pods

    $ kubectl get pods --selector=app=jenkins-pod -o yaml | grep "podIP:"

### References

+ [kubectlチートシート](https://kubernetes.io/ja/docs/reference/kubectl/cheatsheet/)
+ [実行中のコンテナへのシェルを取得する](https://kubernetes.io/ja/docs/tasks/debug-application-cluster/get-shell-running-container/)
  + [Get a Shell to a Running Container](https://kubernetes.io/docs/tasks/debug-application-cluster/get-shell-running-container/)