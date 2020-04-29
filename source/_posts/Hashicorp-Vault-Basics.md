---
title: Hashicorp Vault Basics
date: 2019-10-18 14:35:47
tags: [Hashicorp, Vault]
categories: [Ops, Vault]
---
![Vault](https://philsblog.b-cdn.net/images/vault.png "Vault")


# Install Hashicorp vault on GCP
There is a existing module provided



[terraform-google-modules/vault/google](https://github.com/terraform-google-modules/terraform-google-vault, "Vault on GCE Terraform Module")

Follow the instruction of this module, there are some minor issues though, not sure if it is fixed or not, I will provide how I install it here.

1. add the following module to your main.tf
```bash
module "vault" {
  source         = "terraform-google-modules/vault/google"
  project_id     = var.project_id
  region         = var.region
  kms_keyring    = var.kms_keyring
  kms_crypto_key = var.kms_crypto_key
}

output "vault_addr" {
  value = module.vault.vault_addr
}
```

2. tf apply
3. export these two variable which will be picked up by **vault**, the name of the output should match the one defined in your main.tf
```bash
$ export VAULT_ADDR="$(terraform output vault_address)"
$ export VAULT_CACERT="$(pwd)/ca.crt"
```

4. init your cluster, it basically shard a key into 5 pieces, to unseal the vault, you will need at least provide any 3 of the 5. Change the number to your liking, the default recommendation are 5 and 3. It will also generate the root token along with the unseal key. Save then somewhere safe.
```bash
$ vault operator init \
    -recovery-shares 5 \
    -recovery-threshold 3
```

# Most used commands
```bash
vault operator init -recovery-shares 5 -recovery-threshold 3
```
```bash
vault login
```
```bash
vault audit enable file file_path=/var/log/vault/audit.log
```
```bash
vault secrets list -detailed
```
```bash
vault secrets enable -path=secret secret
vault secrets enable -path=secret/ kv
vault secrets enable kv-v2
vault secrets enable -path=secret/ -version=2 kv
```
```bash
vault kv enable-versioning secret/
```
```bash
vault secrets list -detailed
```
```bash
vault kv put secret/hello foo=world
vault kv put secret/apikey/splunk apikey="xxxxxx"
# $cat acme.json{
#     "organization" : "xxx",
#     "region": "bla",
#     "zip_code": "bla",
#     "contact_email": "bla"
# }
vault kv put secret/customer.acme @acme.json
vault kv get -field=contact_email secret/customer/acme
```
```bash
vault kv put secret/customer/acme contact_email="jennifer@acme.com"
```
put is a replacement, it's not a merge. All the data will be overwriten after put, e.g. in the above json example, organization and region are lost if doing put
it also keeps a different version
```bash
vault kv patch secret/customer/acme contact_email="jennifer@acme.com"
```
just update one field in the secret, use patch. No patch equivlant api yet, it is a wrap of many other command, do the hard work for you.
```bash
vault kv delete secret/apikey/splunk
```
if using version 1, then it is deleted, if usinv version 2, then the secrets are just marked as deleted.
if you want to really delete the secret in version 2, do a destroy
```bash
vault kv destroy secret/apikey/splunk
```
```bash
vault kv etadata delete secret/apikey/splunk

```
example of using apis
```bash
$curl --header "X-Vault-Token:<tken>" \
      --request POST \ 
      --data '{ "apikey": "3230falksj2jsd" }'
      https://vault.rocks/v1/secret/apikey/splunk

$curl --header "X-Vault-Token:<tken>" \
      --request GET \ 
      https://vault.rocks/v1/secret/apikey/splunk

$curl --header "X-Vault-Token:<tken>" \
      --request DELETE \ 
      https://vault.rocks/v1/secret/apikey/splunk

# if you are using kv 2, then url will have a "data" in the middle
$curl --header "X-Vault-Token:<tken>" \
      --request DELETE \ 
      https://vault.rocks/v1/secret/data/apikey/splunk
```
CHeck and set, only for kv-v2
tell the engine, alert the user when changing the secret
enable it on the secret engine mounted at secret
```bash
vault write secret/config cas-required=true
```
enable it only on the secret/partner path
```bash
vault kv metadata put -cas-required=true secret/partner
```
when check and set is enabled, every write operation requres cas value, set the cas to 0 if the write should be allowed only if the key does not exist. Otherwise, set it to the current versin number.
```bash
vault kv put -cas=3 secret/apikey admin-key="fasjdfslkjf"
```
UI is actually nicer if you want to do versioning, in UI, you can create a new version based on a seleceted history version.
```bash
vault kv get secret/hello
```

# Cubbyhole

* used to store arbitrary secrets
* enabled by default at **thecubbyhole/path**
* Every little slot is dedicated to an individual user.
* Its lifetime is linked to the token used to write the data, no TTL in cubbyhole
* Even root cannot read the data if it wasn't written by the root
* Cubbyhole secret engine cannot be disabled, moved or enabled multiple times

vault write cubbyhole/github_token token="1234121"
vault read cubbyhole/github_token

$curl --header "X-Vault-Token:<token>"
      --request POST \
      --data '{"token": "1234643252342"}'
      https://vault.rocks/v1/cubyhole/github_token
## response wrapping


# Dynamic Secrets
dynamic secrets are generated when they are accessed, they do not exist until they are read, so there is no risk of someone stealing them, or another client using the same secrets.