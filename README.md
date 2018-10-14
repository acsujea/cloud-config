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
6. use vault cli to write data
  vault write "$generic"/dss/common key1=value1 key2=value2
7. use vault clie to read data
  vault read "$generic"/dss/common
8. use vault cli to create dss transit key ring
  vault write -f "$generic"/keys/dssKeyRing
9. use vault cli to encrypt data
  vault write -f "$transit"/encrypt/dssKeyRing plaintext="$base64 encoded valute"
10. use vault cli to decrypt data
 vault write -f "$transit"/decrypt/dssKeyRing ciphertext="$ciphertest"
11. use base64 decode to decode above decrypted value.
