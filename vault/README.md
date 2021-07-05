# Vault Helm Chart

> :warning: **Please note**: We take Vault's security and our users' trust very seriously. If 
you believe you have found a security issue in Vault Helm, _please responsibly disclose_ 
by contacting us at [security@hashicorp.com](mailto:security@hashicorp.com).

This repository contains the official HashiCorp Helm chart for installing
and configuring Vault on Kubernetes. This chart supports multiple use
cases of Vault on Kubernetes depending on the values provided.

For full documentation on this Helm chart along with all the ways you can
use Vault with Kubernetes, please see the
[Vault and Kubernetes documentation](https://www.vaultproject.io/docs/platform/k8s/).

## Prerequisites

To use the charts here, [Helm](https://helm.sh/) must be configured for your
Kubernetes cluster. Setting up Kubernetes and Helm is outside the scope of
this README. Please refer to the Kubernetes and Helm documentation.

The versions required are:

  * **Helm 3.0+** - This is the earliest version of Helm tested. It is possible
    it works with earlier versions but this chart is untested for those versions.
  * **Kubernetes 1.14+** - This is the earliest version of Kubernetes tested.
    It is possible that this chart works with earlier versions but it is
    untested.

## Usage

To install the latest version of this chart, add the Hashicorp helm repository
and run `helm install`:

```console
$ helm repo add hashicorp https://helm.releases.hashicorp.com
"hashicorp" has been added to your repositories

$ helm install vault hashicorp/vault
```

Please see the many options supported in the `values.yaml` file. These are also
fully documented directly on the [Vault
website](https://www.vaultproject.io/docs/platform/k8s/helm) along with more
detailed installation instructions.


# Manaul steps to be taken after helm chart install. 

# Check pod vault is running on pod (Kubectl get pod should show it as not ready)

  kubectl exec -it vault-0 -- vault -h (This is running the "vault help" command inside of the container)

# The vault server need to be initialized, the initialization generates the cred to unseal vault

  kubectl exec vault-0 -- vault operator init -format=json > cluster-keys.json (This will output the keys to a file called cluster-keys.json at your current direcotry)

# Unseal vault 

  Run the following to get the keyts from the above file:

    cat cluster-keys.json | jq -r ".unseal_keys_b64[]"

  Now applly one key to the variable

    VAULT_UNSEAL_KEY=$key from above

  Now run this command to start the unseal process
    kubectl exec vault-0 -- vault operator unseal $VAULT_UNSEAL_KEY

# Log into container adn then Vault

  In order for you to perform more vault command log into the vaul container with the following command

    kubectl exec -it vault-0 -- sh  

  Now you need to log into the vault with the inital key you got from the cluster-keys.json file from before

    Vault login

  Now provide the inital key and you will be authenticated with vault

#  



