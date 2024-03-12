## Using ArgoCD to Deploy the 'apps-of-apps' Application

### Prerequisites

- Ensure you have ArgoCD installed and configured in your Kubernetes cluster. Refer to the [ArgoCD documentation](https://argoproj.github.io/argo-cd/) for installation instructions.

## Setting up the NEO4J_AUTH value
To set up the `NEO4J_AUTH` value, follow these steps:

### 1. Encode your username and password:

If your username is `neo4j` and your password is `mypassword`, the string to be encoded would be `neo4j:mypassword`.

### 2. Base64 encode the string:

Use a tool or command to base64 encode the string. For example, you can use the `base64` command in Unix-like systems:

```bash
echo -n 'neo4j:mypassword' | base64
```
This would output the base64 encoded string, which you'll need in the next step.

### 3. Prepend `neo4j/`:

After obtaining the base64 encoded string, prepend `neo4j/` to it.
For example, if the base64 encoded string is `bmVvNGo6bXlwYXNzd29yZA==`, then the `NEO4J_AUTH` value would be `neo4j/bmVvNGo6bXlwYXNzd29yZA==`.

Ensure to replace `neo4j` with your actual username and `mypassword` with your actual password. Additionally, use the appropriate method to base64 encode the string based on your operating system.

### 4. Creating the Kubernetes Secret 

After obtaining the `NEO4J_AUTH` value, you can create a Kubernetes Secret to store it. Use the following command: 
```bash
kubectl create secret generic neo4j-auth \
--namespace=neo4j\
--from-literal=NEO4J_AUTH=neo4j/bmVvNGo6bXlwYXNzd29yZA==
```

## Apply the manifest
```bash
kubectl apply -f https://raw.githubusercontent.com/GBrunelli/neo4j-argocd-cluster-template/master/argocd-apps/neo4j.yaml
```
