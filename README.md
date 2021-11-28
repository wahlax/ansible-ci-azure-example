# Terraform on Azure with CI built from Ansible

Builds VM instance on Azure provisioned by ansible. 2 entry points exist:
  * Jenkinsfile - configured for use with @wahlax/ansible-ci
  * Local ansible pipeline - use ansible-vault for credentials

Example using local ansible pipeline and vault to supply Azure credentials to terraform

```
ansible-playbook -i inventory.ini pipeline.yml -e "ci_work_dir=`pwd`" -e "@vault/secrets.yml" --vault-password-file vault/password-file
```

## Vault Credentials

  * `azure-client-id` - client id for azure provisioning
  * `azure-client-secret` - client secret for azure provisioning
  * `azure-subscription-id` - subscription id for azure provisioning
  * `azure-tenant-id` - tenant for azure provisioning

## Files

  * `Jenkinsfile` - entry point when used with jenkins ci
  * `pipeline.yml` - entry point for ansible (jenkins alternative)
  * `terraform-env.shl` - sets env for terraform
  * `inventory.ini` - defines localhost only right now
  * `main.tf` - aws infra definition in terraform
  * `provisioner.yml` - ansible provisioner used by terraform
  * `requirements.yml` - dependencies of ansible provisioner

## Notes

 * Ansible provisioner failed to connect immediately on azure with dynamic ip. Might prefer building inventory from terraform output and provision in next play.
