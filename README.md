
# OCCM version 1.27

In this directory we store the three yaml files necessary for the configuration of the Kubernetes Openstack Cloud Controller Manager (OCCM), version 1.27.
The reference link of this version is the following: https://github.com/kubernetes/cloud-provider-openstack/blob/release-1.27/docs/openstack-cloud-controller-manager/using-openstack-cloud-controller-manager.md

These files should be added in a section `addons_include` in the RKE Template file used for the creation of the cluster; you should also remember to configure the `cloud-config` secret with the application credentials in order to use it.

The three files here stored were originally downloaded from the following links (which refers to files inside that git repository):
- https://raw.githubusercontent.com/kubernetes/cloud-provider-openstack/master/manifests/controller-manager/cloud-controller-manager-roles.yaml
- https://raw.githubusercontent.com/kubernetes/cloud-provider-openstack/master/manifests/controller-manager/cloud-controller-manager-role-bindings.yaml
- https://raw.githubusercontent.com/kubernetes/cloud-provider-openstack/master/manifests/controller-manager/openstack-cloud-controller-manager-ds.yaml

List of adjustments made on the original files:
- In the file `openstack-cloud-controller-manager-ds.yaml`, line 28, under `spec: template: spec: nodeSelector:`, the label `node-role.kubernetes.io/control-plane: ""` must be substituted with `node-role.kubernetes.io/control-plane: "true"`


License

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
