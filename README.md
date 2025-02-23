<a href="https://lacework.com"><img src="https://techally-content.s3-us-west-1.amazonaws.com/public-content/lacework_logo_full.png" width="600"></a>

# terraform-kubernetes-agent

[![GitHub release](https://img.shields.io/github/release/lacework/terraform-kubernetes-agent.svg)](https://github.com/lacework/terraform-kubernetes-agent/releases/)
[![Codefresh build status](https://g.codefresh.io/api/badges/pipeline/lacework/terraform-modules%2Ftest-compatibility?type=cf-1&key=eyJhbGciOiJIUzI1NiJ9.NWVmNTAxOGU4Y2FjOGQzYTkxYjg3ZDEx.RJ3DEzWmBXrJX7m38iExJ_ntGv4_Ip8VTa-an8gBwBo)](https://g.codefresh.io/pipelines/edit/new/builds?id=607e25e6728f5a6fba30431b&pipeline=test-compatibility&projects=terraform-modules&projectId=607db54b728f5a5f8930405d)

A Terraform Module to create a Secret and DaemonSet for deploying the Lacework Datacollector Agent in a Kubernetes cluster.  Optionally, the module can also deploy the Kubernetes Compliance
collection agent.

## Kubernetes

The `main.tf` file will configure a Kubernetes Secret and DaemonSet which will then be used to run the Lacework Datacollector pod across all worker nodes in a cluster.

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.14 |
| <a name="requirement_kubernetes"></a> [kubernetes](#requirement\_kubernetes) | >= 2.0.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_kubernetes"></a> [kubernetes](#provider\_kubernetes) | >= 2.0.0 |
| <a name="provider_random"></a> [random](#provider\_random) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [kubernetes_cluster_role.lacework_k8s_collector](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/cluster_role) | resource |
| [kubernetes_cluster_role_binding.lacework_k8s_collector](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/cluster_role_binding) | resource |
| [kubernetes_daemonset.lacework_datacollector](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/daemonset) | resource |
| [kubernetes_deployment.lacework_k8s_collector](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/deployment) | resource |
| [kubernetes_secret.lacework_access_token](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/secret) | resource |
| [kubernetes_secret.lacework_config](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/secret) | resource |
| [kubernetes_secret.lacework_k8s_collector](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/secret) | resource |
| [kubernetes_service_account.lacework_k8s_collector](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs/resources/service_account) | resource |
| [random_id.cluster_config_name_tail](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/id) | resource |
| [random_id.node_config_name_tail](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/id) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_enable_cluster_agent"></a> [enable\_cluster\_agent](#input\_enable\_cluster\_agent) | A boolean representing whether the Lacework cluster agent should be deployed | `bool` | `false` | no |
| <a name="input_lacework_access_token"></a> [lacework\_access\_token](#input\_lacework\_access\_token) | The access token for the Lacework agent | `string` | n/a | yes |
| <a name="input_lacework_agent_autoupgrade"></a> [lacework\_agent\_autoupgrade](#input\_lacework\_agent\_autoupgrade) | Boolean value to control whether or not the agent should automatically upgrade to newer versions when available | `bool` | `true` | no |
| <a name="input_lacework_agent_configuration"></a> [lacework\_agent\_configuration](#input\_lacework\_agent\_configuration) | A map/dictionary of configuration parameters for the Lacework datacollector | `any` | `{}` | no |
| <a name="input_lacework_agent_interface_connection_size"></a> [lacework\_agent\_interface\_connection\_size](#input\_lacework\_agent\_interface\_connection\_size) | Desired value for the InterfaceConnectionSize Lacework agent parameter | `string` | `""` | no |
| <a name="input_lacework_agent_log_stdout"></a> [lacework\_agent\_log\_stdout](#input\_lacework\_agent\_log\_stdout) | Enable Lacework agent stdout logging. | `bool` | `true` | no |
| <a name="input_lacework_agent_name"></a> [lacework\_agent\_name](#input\_lacework\_agent\_name) | The name for the Lacework agent service within Kubernetes | `string` | `"lacework-agent"` | no |
| <a name="input_lacework_agent_tags"></a> [lacework\_agent\_tags](#input\_lacework\_agent\_tags) | A map/dictionary of Tags to be assigned to the Lacework datacollector | `map(string)` | `{}` | no |
| <a name="input_lacework_cluster_configuration"></a> [lacework\_cluster\_configuration](#input\_lacework\_cluster\_configuration) | A map/dictionary of configuration parameters for the Lacework K8s collector | `map(any)` | `{}` | no |
| <a name="input_lacework_cluster_cpu_limit"></a> [lacework\_cluster\_cpu\_limit](#input\_lacework\_cluster\_cpu\_limit) | The limit of CPU units for the Lacework K8s collector pod | `string` | `"500m"` | no |
| <a name="input_lacework_cluster_cpu_request"></a> [lacework\_cluster\_cpu\_request](#input\_lacework\_cluster\_cpu\_request) | The amount of CPU units to request for the Lacework K8s collector pod | `string` | `"200m"` | no |
| <a name="input_lacework_cluster_exclusive"></a> [lacework\_cluster\_exclusive](#input\_lacework\_cluster\_exclusive) | A boolean representing whether the Lacework K8s collector will operate in exclusive mode | `bool` | `false` | no |
| <a name="input_lacework_cluster_image"></a> [lacework\_cluster\_image](#input\_lacework\_cluster\_image) | The name of the image to use for deploying the Lacework K8s collector | `string` | `"lacework/k8scollector"` | no |
| <a name="input_lacework_cluster_image_pull_policy"></a> [lacework\_cluster\_image\_pull\_policy](#input\_lacework\_cluster\_image\_pull\_policy) | The pull policy to use for deploying the Lacework K8s collector | `string` | `"Always"` | no |
| <a name="input_lacework_cluster_mem_limit"></a> [lacework\_cluster\_mem\_limit](#input\_lacework\_cluster\_mem\_limit) | The limit of Memory for the Lacework K8s collector pod | `string` | `"1450Mi"` | no |
| <a name="input_lacework_cluster_mem_request"></a> [lacework\_cluster\_mem\_request](#input\_lacework\_cluster\_mem\_request) | The amount of Memory to request for the Lacework K8s collector pod | `string` | `"512Mi"` | no |
| <a name="input_lacework_cluster_name"></a> [lacework\_cluster\_name](#input\_lacework\_cluster\_name) | The name of the K8s cluster that the Lacework K8s collector will monitor | `string` | `""` | no |
| <a name="input_lacework_cluster_region"></a> [lacework\_cluster\_region](#input\_lacework\_cluster\_region) | The region of the K8s cluster that the Lacework K8s collector will monitor | `string` | `""` | no |
| <a name="input_lacework_cluster_type"></a> [lacework\_cluster\_type](#input\_lacework\_cluster\_type) | The type of the K8s cluster that the Lacework K8s collector will monitor | `string` | `""` | no |
| <a name="input_lacework_config_name"></a> [lacework\_config\_name](#input\_lacework\_config\_name) | The name for the Lacework agent configuration within Kubernetes | `string` | `"lacework-config"` | no |
| <a name="input_lacework_enable_default_syscall_config"></a> [lacework\_enable\_default\_syscall\_config](#input\_lacework\_enable\_default\_syscall\_config) | A flag to enable the default syscall config | `bool` | `false` | no |
| <a name="input_lacework_image"></a> [lacework\_image](#input\_lacework\_image) | The name of the image to use for deploying the Lacework datacollector | `string` | `"lacework/datacollector"` | no |
| <a name="input_lacework_image_pull_policy"></a> [lacework\_image\_pull\_policy](#input\_lacework\_image\_pull\_policy) | The pull policy to use for deploying the Lacework datacollector | `string` | `"Always"` | no |
| <a name="input_lacework_proxy_url"></a> [lacework\_proxy\_url](#input\_lacework\_proxy\_url) | The proxy URL for the Lacework agent | `string` | `""` | no |
| <a name="input_lacework_server_url"></a> [lacework\_server\_url](#input\_lacework\_server\_url) | The server URL for the Lacework agent | `string` | `""` | no |
| <a name="input_namespace"></a> [namespace](#input\_namespace) | The Kubernetes namespace in which to deploy | `string` | `"default"` | no |
| <a name="input_node_selector"></a> [node\_selector](#input\_node\_selector) | A map of key:value pairs of node labels to specify which nodes to deploy the DaemonsSet to | `map(any)` | `null` | no |
| <a name="input_pod_cpu_limit"></a> [pod\_cpu\_limit](#input\_pod\_cpu\_limit) | The limit of CPU units for the Lacework datacollector pod | `string` | `"500m"` | no |
| <a name="input_pod_cpu_request"></a> [pod\_cpu\_request](#input\_pod\_cpu\_request) | The amount of CPU units to request for the Lacework datacollector pod | `string` | `"200m"` | no |
| <a name="input_pod_mem_limit"></a> [pod\_mem\_limit](#input\_pod\_mem\_limit) | The limit of Memory for the Lacework datacollector pod | `string` | `"1450Mi"` | no |
| <a name="input_pod_mem_request"></a> [pod\_mem\_request](#input\_pod\_mem\_request) | The amount of Memory to request for the Lacework datacollector pod | `string` | `"512Mi"` | no |
| <a name="input_pod_priority_class_name"></a> [pod\_priority\_class\_name](#input\_pod\_priority\_class\_name) | Indicates the pod's priority. Requires an existing priority class name resource if not 'system-node-critical' and 'system-cluster-critical' | `string` | `""` | no |
| <a name="input_pod_service_account"></a> [pod\_service\_account](#input\_pod\_service\_account) | The Kubernetes ServiceAccount to use in the pod template | `string` | `""` | no |
| <a name="input_revision_history_limit"></a> [revision\_history\_limit](#input\_revision\_history\_limit) | The number of revision hitory to keep. | `number` | `10` | no |
| <a name="input_tolerations"></a> [tolerations](#input\_tolerations) | A list of Kubernetes Tolerations to apply to the DaemonSet definition | `list(map(string))` | <pre>[<br>  {<br>    "effect": "NoSchedule",<br>    "key": "node-role.kubernetes.io/infra"<br>  },<br>  {<br>    "effect": "NoSchedule",<br>    "key": "node-role.kubernetes.io/master"<br>  }<br>]</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_lacework_config_name"></a> [lacework\_config\_name](#output\_lacework\_config\_name) | Name of the Kubernetes Secret containing the Lacework config |
| <a name="output_lacework_config_version"></a> [lacework\_config\_version](#output\_lacework\_config\_version) | Version of the Kubernetes Secret containing the Lacework config |
| <a name="output_lacework_datacollector_name"></a> [lacework\_datacollector\_name](#output\_lacework\_datacollector\_name) | Name of the Kubernetes DaemonSet for the Lacework datacollector |
| <a name="output_lacework_datacollector_version"></a> [lacework\_datacollector\_version](#output\_lacework\_datacollector\_version) | Version of the Kubernetes DaemonSet for the Lacework datacollector |
<!-- END_TF_DOCS -->