---
title: "azure kubernetes service"
component: "Document Editor"
description: "Learn about deploy the Web API controller docker image in Azure Kubernetes Service"
---
# How to deploy word-processor-server Docker container in Azure Kubernetes Service

## Prerequisites

* Have [`Azure account`](https://azure.microsoft.com/en-gb/) and [`Azure CLI`](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) setup in your environment.

* Run the following command to open the Azure login page. Sign into your [`Microsoft Azure account`](https://azure.microsoft.com/en-gb/).

```azurecli
az login
```

**Step 1:** Create a resource group.

Create a resource group using the [`az group create`](https://docs.microsoft.com/en-us/cli/azure/group#az-group-create) command.

The following example creates a resource group named documenteditorresourcegroup in the eastus location.

```azurecli
az group create --name documenteditorresourcegroup --location "East US"
```

**Step 2:** Create AKS cluster.

Use the [`az aks create`](https://docs.microsoft.com/en-us/cli/azure/aks?view=azure-cli-latest#az-aks-create) command to create an AKS cluster. The following example creates a cluster named documenteditorcluster with one node.

```azurecli
az aks create --resource-group documenteditorresourcegroup --name documenteditorcluster --node-count 1
```

**Step 3:** Connect to the cluster.

Install the [`kubectl`](https://kubernetes.io/docs/reference/kubectl/kubectl/) into the workspace using the following command.

```azurecli
az aks install-cli
```

To configure kubectl to connect to your Kubernetes cluster, use the [`az aks get-credentials`](https://docs.microsoft.com/en-us/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```azurecli
az aks get-credentials --resource-group documenteditorresourcegroup --name documenteditorcluster
```

**Step 4:** Create Kubernetes Services and Deployments

[`Kubernetes Services`](https://kubernetes.io/docs/concepts/services-networking/service/) and [`Deployments`](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) can be configured in a file. To run the Document Editor server, you must define a Service and a Deployment documenteditorserver. To do this, create the documenteditor-server.yml file in the current directory using the following code.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: documenteditorserver
  name: documenteditorserver
spec:
  replicas: 1
  selector:
    matchLabels:
      app: documenteditorserver
  strategy: {}
  template:
    metadata:
      labels:
        app: documenteditorserver
    spec:
      containers:
      - image: syncfusion/word-processor-server:latest
        name: documenteditorserver
        ports:
        - containerPort: 80
        env:
        - name: SYNCFUSION_LICENSE_KEY
          value: "YOUR_LICENSE_KEY"
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: documenteditorserver
  name: documenteditorserver
spec:
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: documenteditorserver
  type: LoadBalancer
```

**Step 5:** To create all Services and Deployments needed to run the Document Editor server, execute the following.

```console
kubectl create -f ./documenteditor-server.yml
```

Run the following command to get the Kubernetes cluster deployed service details and copy the external IP address of the Document Editor service.

```console
kubectl get all
```

Browse the copied external IP address and navigate to the Document Editor Web API control `http://<external-ip>/api/documenteditor`. It returns the default get method response.

**Step 6:** Append the Kubernetes service running the URL `http://<external-ip>/api/documenteditor/` to the service URL in the client-side Document Editor control. For more information about the Document Editor control, refer to this [`getting started page`](https://ej2.syncfusion.com/javascript/documentation/document-editor/getting-started).

For more details about the Azure Kubernetes service, please look deeper into [`Microsoft Azure Kubernetes Service`](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough) for a production-ready setup.
