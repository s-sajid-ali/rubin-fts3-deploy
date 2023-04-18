# rubin-fts3-deploy
## Deployment framework for Rubin USDF FTS3. 

Once you have access to your Kubernetes cluster, you can deploy FTS3 for a given overlay (found in overlays/[dev,prod]) using the Makefile found there with (most simply)

    make apply

This will run multiple steps, downloading Secrets from Vault and ending up using Kustomize to create or update `fts3` and `fts3-db` namespaces and the resources to run an FTS3 application in those namespaces. FTS3 application containers will run in the `fts3` namespace, while the `fts3-db` namespace is used for a MariaDB Kubernetes operator managed MySQL-compliant database.

This framework uses `kustomize` to allow modification of YAML templates at deployment time. This is used in particular to patch the environment of containers such that they are configured to have the database connection string passed in via the value of a `Secret`. This allows us to keep the Kubernetes resource manifests under version control, without exposing a base64 encoded password as compared with a `--values` injection to the Helm template process.

Before deploying FTS3, the secrets and credentials needed for the application will need to be pushed to Vault. Vault-resident secrets may then be downloaded (provided you are properly logged into Vault) when `make apply` is run, and then loaded into the cluster via `SecretGenerator` definitions in the `kustomization.yaml` files. 

Be **very** careful with the `make destroy` (commented out of the Makefile by default) command. It will delete absolutely everything, including your database `PersistentVolume` objects.
