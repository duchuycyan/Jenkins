# Cài đặt Jenkins trên Kubernetes Cluster
## **1) Giới thiệu**
- Cài đặt **Jenkins** trên một **Kubernetes Cluster** cực kỳ thuận lợi cho các Kubernetes-based deployments và các dynamic container-based scalable Jenkins agents.
## **2) Các bước cài đặt**
- **B1 :** Khởi tạo namespace cho **Jenkins** :
    ```
    # kubectl create namespace jenkins
    ```
- **B2 :** Tạo file `serviceAccount.yaml` chứa các thông tin về ServiceAccount, ClusterRole và ClusterRoleBinding cần khởi tạo :
    ```yaml
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: jenkins
      namespace: jenkins

    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRole
    metadata:
      name: jenkins-admin
    rules:
      - apiGroups: [""]
        resources: ["*"]
        verbs: ["*"]

    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: jenkins-admin
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: jenkins-admin
    subjects:
    - kind: ServiceAccount
      name: jenkins
      namespace: jenkins
    ```
    > Ở đây, clusterRole `jenkins-admin` có tất cả các quyền quản trị các thành phần trong cluster. Có thể giới hạn quyền bằng các resource action cụ thể.
    - Tạo các resource trên :
        ```
        # kubectl apply -f serviceAccount.yaml
        ```
- **B3 :**