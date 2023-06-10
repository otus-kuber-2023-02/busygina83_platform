$ helm status vault
NAME: vault
LAST DEPLOYED: Sat Jun  3 19:37:01 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
Thank you for installing HashiCorp Vault!

Now that you have deployed Vault, you should look over the docs on using
Vault with Kubernetes available here:

https://www.vaultproject.io/docs/


Your release is named vault. To learn more about the release, try:

  $ helm status vault
  $ helm get manifest vault


$ kubectl exec -it vault-0 -- vault operator init --key-shares=1 --key-threshold=1
Unseal Key 1: bdqlnK6jWdON6UKvHhf2xv7iZjpktR1IWKjTuJ5xHfU=

Initial Root Token: hvs.CHQLgIDjE53GLfR3j6GXTOlm


$ kubectl exec -it vault-0 -- vault operator unseal
Unseal Key (will be hidden):
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.13.1
Build Date      2023-03-23T12:51:35Z
Storage Type    consul
Cluster Name    vault-cluster-9e5968dc
Cluster ID      1820eed2-2e63-4dcc-3cd3-bf4a235f4220
HA Enabled      true
HA Cluster      https://vault-0.vault-internal:8201
HA Mode         active
Active Since    2023-06-03T17:12:50.885727479Z

$ kubectl exec -it vault-1 -- vault operator unseal
Unseal Key (will be hidden):
Key                    Value
---                    -----
Seal Type              shamir
Initialized            true
Sealed                 false
Total Shares           1
Threshold              1
Version                1.13.1
Build Date             2023-03-23T12:51:35Z
Storage Type           consul
Cluster Name           vault-cluster-9e5968dc
Cluster ID             1820eed2-2e63-4dcc-3cd3-bf4a235f4220
HA Enabled             true
HA Cluster             https://vault-0.vault-internal:8201
HA Mode                standby
Active Node Address    http://10.112.7.46:8200

$ kubectl exec -it vault-2 -- vault operator unseal
Unseal Key (will be hidden):
Key                    Value
---                    -----
Seal Type              shamir
Initialized            true
Sealed                 false
Total Shares           1
Threshold              1
Version                1.13.1
Build Date             2023-03-23T12:51:35Z
Storage Type           consul
Cluster Name           vault-cluster-9e5968dc
Cluster ID             1820eed2-2e63-4dcc-3cd3-bf4a235f4220
HA Enabled             true
HA Cluster             https://vault-0.vault-internal:8201
HA Mode                standby
Active Node Address    http://10.112.7.46:8200



$ kubectl exec -it vault-0 -- vault status
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.13.1
Build Date      2023-03-23T12:51:35Z
Storage Type    consul
Cluster Name    vault-cluster-9e5968dc
Cluster ID      1820eed2-2e63-4dcc-3cd3-bf4a235f4220
HA Enabled      true
HA Cluster      https://vault-0.vault-internal:8201
HA Mode         active
Active Since    2023-06-03T17:12:50.885727479Z

$ kubectl exec -it vault-1 -- vault status
Key                    Value
---                    -----
Seal Type              shamir
Initialized            true
Sealed                 false
Total Shares           1
Threshold              1
Version                1.13.1
Build Date             2023-03-23T12:51:35Z
Storage Type           consul
Cluster Name           vault-cluster-9e5968dc
Cluster ID             1820eed2-2e63-4dcc-3cd3-bf4a235f4220
HA Enabled             true
HA Cluster             https://vault-0.vault-internal:8201
HA Mode                standby
Active Node Address    http://10.112.7.46:8200

$ kubectl exec -it vault-2 -- vault status
Key                    Value
---                    -----
Seal Type              shamir
Initialized            true
Sealed                 false
Total Shares           1
Threshold              1
Version                1.13.1
Build Date             2023-03-23T12:51:35Z
Storage Type           consul
Cluster Name           vault-cluster-9e5968dc
Cluster ID             1820eed2-2e63-4dcc-3cd3-bf4a235f4220
HA Enabled             true
HA Cluster             https://vault-0.vault-internal:8201
HA Mode                standby
Active Node Address    http://10.112.7.46:8200



$ kubectl exec -it vault-0 -- vault auth list
Path      Type     Accessor               Description                Version
----      ----     --------               -----------                -------
token/    token    auth_token_7227e27b    token based credentials    n/a



$ kubectl exec -it vault-0 -- vault read otus/otus-ro/config
Key                 Value
---                 -----
refresh_interval    768h
password            asajkjkahs
username            otus

$ kubectl exec -it vault-0 -- vault kv get otus/otus-rw/config
====== Data ======
Key         Value
---         -----
password    asajkjkahs
username    otus



$ kubectl exec -it vault-0 -- vault auth list
Path           Type          Accessor                    Description                Version
----           ----          --------                    -----------                -------
kubernetes/    kubernetes    auth_kubernetes_88d3b88a    n/a                        n/a
token/         token         auth_token_7227e27b         token based credentials    n/a



# добавляем  "update"
$ kubectl exec -it vault-0 -- cat /home/vault/otus-policy.hcl
path "otus/otus-ro/*" {
  capabilities = ["read", "list"]
}
path "otus/otus-rw/*" {
  capabilities = ["read", "create", "update", "list"]
}



$ kubectl exec -it vault-0 -- vault write pki_int/issue/example-dot-ru common_name="test.example.ru" ttl="24h"
Key                 Value
---                 -----
ca_chain            [-----BEGIN CERTIFICATE-----
...

