ty SRE 수업 중 kube-ops-view를 kubernetes에 반영하는 것을 목표로 한다.




## ops-view.yaml
kubernetes 대상으로 Deployment와 Service를 정의한다.



## kube-ops-view-rbac.yaml
kube-ops-view가 kubernetes cluster의 information을 가져올 수 있도록
권한을 정의한다.

- namespace: udacity
- ServiceAccount
- ClusterRole
  - nodes와 pods의 resources를 접근 가능하다
  - get과 list를 조회할 수 있다.
- ClusterRoleBinding



## 권한 정의
kubernetes에서 새로운 namespace를 만들경우 default 권한을 pod에 주게 된다.
이 default 권한은 아무런 cluster 조회 권한이 없음으로
ops-view와 같은 cluster info를 조회하는 목적의 software가 정상 작동을 하지 못한다.



```
$ kubectl get serviceaccount -n udacity
NAME            SECRETS   AGE
default         1         149m
kube-ops-view   1         87m
```

위와 같이 2개의 권한이 있을 경우 serviceAccount를 통해서 user를 지정해 줘야 한다.

