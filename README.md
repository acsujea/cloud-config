# cloud-config

1. create hashicorp vault service
 cf create-service hashicorp-vault shared dss-vault-service -c ../config-service.json
2. verify the creation of vault service to make sure "status:    create succeeded"
 cf service dss-vault-service
3. create service key for this vault service to read/write to the vault
  cf create-service-key dss-vault-service dssVaultServiceKey 
4. get the newly created service key for the vault access information
  cf service-key dss-vault-service dss0VaultServiceKey
5. SET/EXPORT vault address and vault token for vault cli
   SET VAULT_ADDR= the "address" value from service-key
   SET VAULT_TOKEN= the "token" value from service-key

