# Steps to solve Issues related to kepler deployment via helm in K8S cluster deployed via kubeadm

- Deploy Prometheus using Prometheus operator https://sustainable-computing.io/installation/kepler/#deploy-the-prometheus-operator 

- It is better to use the same name space for kepler and Prometheus to avoid access control issues.
  
- changes to be done in the values.yaml  https://github.com/sustainable-computing-io/kepler-helm-chart/blob/main/chart/kepler/values.yaml 

serviceMonitor: <br>
&nbsp;  enabled: true <br>
&nbsp;  namespace: "name of the namespace"<br>
&nbsp;  interval: 30s <br>
&nbsp;  scrapeTimeout: 20s <br>
&nbsp;  labels: {} 
 
**helm install kepler kepler/kepler --values values.yaml --namespace “name of the namespace”**

if you use different namespace for Prometheus and Kepler then deploy also

Prometheus role (modify system namespace to Kepler namespace): https://github.com/sustainable-computing-io/kepler/blob/main/manifests/config/rbac/prometheus_role.yaml
 <br>
  <br>
Prometheus role-binding (modify Kepler and Prometheus namespace): https://github.com/sustainable-computing-io/kepler/blob/main/manifests/config/rbac/prometheus_role_binding.yaml
