# terraform-google-vpc

## Description
### Tagline
This is an auto-generated module.

### Detailed
This module was generated from [terraform-google-module-template](https://github.com/terraform-google-modules/terraform-google-module-template/), which by default generates a module that simply creates a GCS bucket. As the module develops, this README should be updated.

The resources/services/activations/deletions that this module will create/trigger are:

- Create a GCS bucket with the provided name

### PreDeploy
To deploy this blueprint you must have an active billing account and billing permissions.

## Architecture
![alt text for diagram](https://www.link-to-architecture-diagram.com)
1. Architecture description step no. 1
2. Architecture description step no. 2
3. Architecture description step no. N

## Documentation
- [Hosting a Static Website](https://cloud.google.com/storage/docs/hosting-static-website)

## Deployment Duration
Configuration: X mins
Deployment: Y mins

## Cost
[Blueprint cost details](https://cloud.google.com/products/calculator?id=02fb0c45-cc29-4567-8cc6-f72ac9024add)

## Usage

Basic usage of this module is as follows:

```hcl
module "vpc" {
  source  = "terraform-google-modules/vpc/google"
  version = "~> 0.1"

  project_id  = "<PROJECT ID>"
  bucket_name = "gcs-test-bucket"
}
```

Functional examples are included in the
[examples](./examples/) directory.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| additional\_subnetworks | DEPRECATED: please see https://goo.gle/hpc-toolkit-vpc-deprecation for migration instructions | `list(map(string))` | `null` | no |
| allowed\_ssh\_ip\_ranges | A list of CIDR IP ranges from which to allow ssh access | `list(string)` | `[]` | no |
| default\_primary\_subnetwork\_size | The size, in CIDR bits, of the default primary subnetwork unless explicitly defined in var.subnetworks | `number` | `15` | no |
| delete\_default\_internet\_gateway\_routes | If set, ensure that all routes within the network specified whose names begin with 'default-route' and with a next hop of 'default-internet-gateway' are deleted | `bool` | `false` | no |
| deployment\_name | The name of the current deployment | `string` | n/a | yes |
| enable\_iap\_rdp\_ingress | Enable a firewall rule to allow Windows Remote Desktop Protocol access using IAP tunnels | `bool` | `false` | no |
| enable\_iap\_ssh\_ingress | Enable a firewall rule to allow SSH access using IAP tunnels | `bool` | `true` | no |
| enable\_iap\_winrm\_ingress | Enable a firewall rule to allow Windows Remote Management (WinRM) access using IAP tunnels | `bool` | `false` | no |
| enable\_internal\_traffic | Enable a firewall rule to allow all internal TCP, UDP, and ICMP traffic within the network | `bool` | `true` | no |
| extra\_iap\_ports | A list of TCP ports for which to create firewall rules that enable IAP for TCP forwarding (use dedicated enable\_iap variables for standard ports) | `list(string)` | `[]` | no |
| firewall\_log\_config | Firewall log configuration for Toolkit firewall rules (var.enable\_iap\_ssh\_ingress and others) | `string` | `"DISABLE_LOGGING"` | no |
| firewall\_rules | List of firewall rules | `any` | `[]` | no |
| ips\_per\_nat | The number of IP addresses to allocate for each regional Cloud NAT (set to 0 to disable NAT) | `number` | `2` | no |
| mtu | The network MTU (default: 8896). Recommended values: 0 (use Compute Engine default), 1460 (default outside HPC environments), 1500 (Internet default), or 8896 (for Jumbo packets). Allowed are all values in the range 1300 to 8896, inclusively. | `number` | `8896` | no |
| network\_address\_range | IP address range (CIDR) for global network | `string` | `"10.0.0.0/9"` | no |
| network\_description | An optional description of this resource (changes will trigger resource destroy/create) | `string` | `""` | no |
| network\_name | The name of the network to be created (if unsupplied, will default to "{deployment\_name}-net") | `string` | `null` | no |
| network\_routing\_mode | The network routing mode (default "GLOBAL") | `string` | `"GLOBAL"` | no |
| primary\_subnetwork | DEPRECATED: please see https://goo.gle/hpc-toolkit-vpc-deprecation for migration instructions | `map(string)` | `null` | no |
| project\_id | Project in which the HPC deployment will be created | `string` | n/a | yes |
| region | The default region for Cloud resources | `string` | n/a | yes |
| shared\_vpc\_host | Makes this project a Shared VPC host if 'true' (default 'false') | `bool` | `false` | no |
| subnetwork\_size | DEPRECATED: please see https://goo.gle/hpc-toolkit-vpc-deprecation for migration instructions | `number` | `null` | no |
| subnetworks | List of subnetworks to create within the VPC. If left empty, it will be<br>replaced by a single, default subnetwork constructed from other parameters<br>(e.g. var.region). In all cases, the first subnetwork in the list is identified<br>by outputs as a "primary" subnetwork.<br><br>subnet\_name           (string, required, name of subnet)<br>subnet\_region         (string, required, region of subnet)<br>subnet\_ip             (string, mutually exclusive with new\_bits, CIDR-formatted IP range for subnetwork)<br>new\_bits              (number, mutually exclusive with subnet\_ip, CIDR bits used to calculate subnetwork range)<br>subnet\_private\_access (bool, optional, Enable Private Access on subnetwork)<br>subnet\_flow\_logs      (map(string), optional, Configure Flow Logs see terraform-google-network module)<br>description           (string, optional, Description of Network)<br>purpose               (string, optional, related to Load Balancing)<br>role                  (string, optional, related to Load Balancing) | `list(map(string))` | `[]` | no |

## Outputs

| Name | Description |
|------|-------------|
| nat\_ips | External IPs of the Cloud NAT from which outbound internet traffic will arrive (empty list if no NAT is used) |
| network\_id | ID of the new VPC network |
| network\_name | Name of the new VPC network |
| network\_self\_link | Self link of the new VPC network |
| subnetwork | Primary subnetwork object |
| subnetwork\_address | IP address range of the primary subnetwork |
| subnetwork\_name | Name of the primary subnetwork |
| subnetwork\_self\_link | Self link of the primary subnetwork |
| subnetworks | Full list of subnetwork objects belonging to the new VPC network |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

These sections describe requirements for using this module.

### Software

The following dependencies must be available:

- [Terraform][terraform] v0.13
- [Terraform Provider for GCP][terraform-provider-gcp] plugin v3.0

### Service Account

A service account with the following roles must be used to provision
the resources of this module:

- Storage Admin: `roles/storage.admin`

The [Project Factory module][project-factory-module] and the
[IAM module][iam-module] may be used in combination to provision a
service account with the necessary roles applied.

### APIs

A project with the following APIs enabled must be used to host the
resources of this module:

- Google Cloud Storage JSON API: `storage-api.googleapis.com`

The [Project Factory module][project-factory-module] can be used to
provision a project with the necessary APIs enabled.

## Contributing

Refer to the [contribution guidelines](./CONTRIBUTING.md) for
information on contributing to this module.

[iam-module]: https://registry.terraform.io/modules/terraform-google-modules/iam/google
[project-factory-module]: https://registry.terraform.io/modules/terraform-google-modules/project-factory/google
[terraform-provider-gcp]: https://www.terraform.io/docs/providers/google/index.html
[terraform]: https://www.terraform.io/downloads.html

## Security Disclosures

Please see our [security disclosure process](./SECURITY.md).
