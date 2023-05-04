
# OCCM version 1.27

In this directory we store the three yaml files necessary for the configuration of the Kubernetes Openstack Cloud Controller Manager (OCCM), version 1.22.0.
The reference link of this version is the following: https://github.com/kubernetes/cloud-provider-openstack/blob/release-1.22/docs/openstack-cloud-controller-manager/using-openstack-cloud-controller-manager.md

These files should be added in a section `addons_include` in the RKE Template file used for the creation of the cluster; you should also remember to configure the `cloud-config` secret with the application credentials in order to use it.

The three files here stored were originally downloaded from the following links (which refers to files inside that git repository):
- https://raw.githubusercontent.com/kubernetes/cloud-provider-openstack/release-1.22/manifests/controller-manager/cloud-controller-manager-roles.yaml
- https://raw.githubusercontent.com/kubernetes/cloud-provider-openstack/release-1.22/manifests/controller-manager/cloud-controller-manager-role-bindings.yaml
- https://raw.githubusercontent.com/kubernetes/cloud-provider-openstack/release-1.22/manifests/controller-manager/openstack-cloud-controller-manager-ds.yaml

List of adjustments made on the original files in the file `openstack-cloud-controller-manager-ds.yaml`:
- line 27 changed: under `spec: template: spec: nodeSelector:`, the label `node-role.kubernetes.io/master: ""` must be substituted with `node-role.kubernetes.io/controlplane: "true"`
- line 68 changed: in the section `spec: template: spec: containers: - name: env:`, the `value: /etc/config/cloud.conf` has been changed in `value: /etc/config/cloud-config`
- lines 36-41 added: the section `spec: template: spec: toleration:` must be filled with all the following tolerations (only the first two were originally provided):


```yaml
...
spec:
  ...
  template:
  ...
    spec:
      ...
      tolerations:
      - key: node.cloudprovider.kubernetes.io/uninitialized
        value: "true"
        effect: NoSchedule
      - key: node-role.kubernetes.io/master
        effect: NoSchedule
        value: "true"
      - key: node-role.kubernetes.io/controlplane
        effect: NoSchedule
        value: "true"
      - key: node-role.kubernetes.io/etcd
        effect: NoExecute
        value: "true"
```

There are no changes id  `cloud-controller-manager-roles.yaml` and  `cloud-controller-manager-role-bindings.yaml`


## License

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
