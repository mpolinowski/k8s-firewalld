# k8s-firewalld
Firewalld service configuration files for Kubernetes hosts


Master nodes

| Protocol  | Direction  | Port Range  | Purpose  | Used By  |
|---|---|---|---|---|
|  TCP |  Inbound | 6443  | Kubernetes API server | All  |
|  TCP |  Inbound | 2379-2380  | etcd server client API | kube-apiserver, etcd |
|  TCP |  Inbound | 10250  | Kubelet API | Self, Control plane |
|  TCP |  Inbound | 10251  | kube-scheduler | Self |
|  TCP |  Inbound | 10253  | kube-controller-manager | Self |

				

Worker nodes

| Protocol  | Direction  | Port Range  | Purpose  | Used By  |
|---|---|---|---|---|
|  TCP |  Inbound | 10250  | Kubelet API | Self, Control plane  |
|  TCP |  Inbound | 30000-32767  | NodePort Services | All |


To test on a Kubernetes Master:
<ul>
  <li>Copy the k8s-master.xml file to the /etc/firewalld/services directory</li>
  <li>Reload the firewall daemon with firewall-cmd --reload</li>
  <li>Add the service to the appropriate zone with firewall-cmd --add-service=k8s-master --zone=public</li>
  <liOptionally, make the service permanent with firewall-cmd --runtime-to-permanent</li>
</ul>

To test on a Kubernetes Worker:
<ul>
  <li>Copy the k8s-worker.xml file to the /etc/firewalld/services directory</li>
  <li>Reload the firewall daemon with firewall-cmd --reload</li>
  <li>Add the service to the appropriate zone with firewall-cmd --add-service=k8s-worker --zone=public</li>
  <liOptionally, make the service permanent with firewall-cmd --runtime-to-permanent</li>
</ul>
