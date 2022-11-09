# TerraGoat 
TerraGoat is a learning and training project that demonstrates how common configuration errors can find their way into production cloud environments. AWS, GCP, Azure 

## Config Notes 
*Annotations that deviate from the provided documentation*

```bash
# Must be globally unique in GCP
export TF_TERRAGOAT_STATE_BUCKET=remote-state-bucket-aracely-terragoat

# Must give full path, including filename. Does not accept directory
export TF_VAR_credentials_path=<PATH_TO_CREDNETIALS_FILE> 

```

### `terraform apply` errors 
- [x] Need to enable Cloud SQL Admin API within the project in use 
- [x] Use `_` not `-` ; lowercase only in variables, name
- [x] Update location variable to `us-central1-c` (was `us-central1c`) in `variables.tf`
- [x] Image name is outdated (debian-9). Pick a newer image name and use that 


---
## Evaluation (gcp)
| Criteria | Score | Notes | 
| ------- | ------- | ------ | 
|  Date of last update | 5 | Update in the last few months (from 10/22)| 
| Ease of install | 5 | Simple download of repo in GitHub | 
| Ease of configuration | 3 | Required some tweaking in order to apply to GCP without errors | 
| Ease of use | 3 | Once configuration is tweaked, it should be relatively easy to use (apply and destroy) | 
| Documentation | 3 | Initial documentation to get started exists, but it expects the user to figure the rest out on her own.| 

### Other notes: 
#### Cost estimate (monthly)
*Estimate via Infracost*
![terragoat-cost.png]

