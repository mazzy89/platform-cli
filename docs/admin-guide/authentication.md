1. Install kubectl

`brew install kubernetes-cli`


2. Install kubelogin

```shell
brew tap int128/kubelogin
brew install kubelogin
```
3. Update your ~/.kube/config file

A single-sign on enabled kubeconfig can be generated by the administrator using:

```shell
platform-cli kubeconfig sso
```

or alternatively create one by updating the values below:
```yaml
apiVersion: v1
clusters:
- cluster:
    insecure-skip-tls-verify: true
    server:
  name: cluster
contexts:
- context:
    cluster: cluster
    user: sso
  name: cluster
current-context: cluster
kind: Config
preferences: {}
users:
- name: cluster
  user:
    auth-provider:
      config:
        client-id: <...>
        client-secret: <...>
        extra-scopes: offline_access openid profile email groups
        idp-certificate-authority-data: <...>
        idp-issuer-url: https://dex.{domain}
      name: oidc
```

4. Run `kubelogin` to login with your Active Directory credentials and update your `~/.kube/config`

```shell
kubelogin
```

5. Profit, You may now use kubectl as normal
