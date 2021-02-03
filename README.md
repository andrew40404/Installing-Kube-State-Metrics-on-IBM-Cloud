# Installing Kube-State-Metrics on IBM Cloud

**Step 1 provision Kubernetes Cluster**

- Click the **Catalog** button on the top

- Select **Service** from the **Catalog**

- Search for **Kubernetes Service** and click on it

  ![kube state metrics doc_html_46d1c04e26ba5eea](https://user-images.githubusercontent.com/5286796/106394850-d29c7000-6424-11eb-92f5-40a884eddfab.png)

- You are now at the Kubernetes deployment page. You need to specify some details about the cluster

- Choose a plan **standard** or **free**. The free plan only has one worker node and no subnet. To provision a standard cluster, you will need to upgrade your account to Pay-As-You-Go

- To upgrade to a Pay-As-You-Go account, complete the following steps:

- In the console, go to Manage > Account.

- Select Account settings; and click Add credit card.

- Enter your payment information, click Next, and submit your information

- Choose **classic** or **VPC**. Please read the docs and choose the most suitable type for yourself.

![kube state metrics doc_html_4d3a968071544952](https://user-images.githubusercontent.com/5286796/106394848-d0d2ac80-6424-11eb-93eb-02080615c50a.png)

- Now choose your location settings,

- Choose **Geography** (continent)

![kube state metrics doc_html_72496e6b0b2c820d](https://user-images.githubusercontent.com/5286796/106394846-cf08e900-6424-11eb-9371-8bcd87fb91c5.png)

- Choose 	Single or Multizone. In single zone, your data is only kept on the	datacenter. On the other hand with Multizone, it is distributed to multiple zones, thus safer in an unforeseen zone failure.

- If you wish to use Multizone, please set up your account with VRF

- If at your current location selection, there is no available Virtual LAN, a new VLAN will be created for you
- Choose a Worker node setup or use the preselected one, set Worker node amount per zone
- Choose **Master Service Endpoint**. 

> In VRF-enabled accounts, you can choose private-only to make your master accessible on the private network or via VPN tunnel. Choose public-only to make your master publicly accessible. When you have a VRF-enabled account, your cluster is set up by default to use both private and public endpoints.


- Give desired **tags** to your cluster, for more information visit tags
- Click **create**
  - Wait for your cluster to be provisioned
  - Your cluster is ready for usage

**Step 2 Deploy IBM Cloud Block Storage plug-in**

The Block Storage plug-in is a persistent, high-performance iSCSI storage that you can add to your apps by using Kubernetes Persistent Volumes (PVs).

- Click the **Catalog** button on the top

- Select **Software** from the catalog

- Search for **IBM Cloud Block Storage plug-in** and click on it

![kube state metrics4](https://user-images.githubusercontent.com/5286796/106734578-30090a80-6639-11eb-92f3-b7a9355a89ca.png)

  - On the application page Click in the dot next to the cluster, you wish to use

  - Click on Enter or Select Namespace and choose the default Namespace or use a custom one (if you get error please wait 30 minutes for the cluster to finalize)

![kube state metrics6](https://user-images.githubusercontent.com/5286796/106734562-2c758380-6639-11eb-9497-4ae0a098d824.png)

- Give a **name** to this workspace

- Click **install** and wait for the deployment

![kube state metrics5](https://user-images.githubusercontent.com/5286796/106734574-2ed7dd80-6639-11eb-9be9-cfe10c69a14c.png)

# Step 3 Install The Kube-State-Metrics Chart

- ​	Add the Bitnami repository to Helm with the following command:

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
```

A Helm chart describes a specific version of a solution, also known as a **release**. The **release** include files with Kubernetes-needed resources and files that describe the installation, configuration, usage and license of a chart.

- ​	Check that your Kubernetes cluster is running by executing the following command:

```sh
kubectl cluster-info 
```

> **NOTE**: Remember that `MY-RELEASE` is a placeholder. Please replace it with the name you want to give to the chart or add the `--generate-name` flag to give the chart a random name.

```sh
helm install MY-RELEASE bitnami/kube-state-metrics
```

**Collect resource metrics from Kubernetes objects**

- Deploy **Metrics Server**.
- Use **kubectl** get to query the **Metrics** API
- View **metric** snapshots using **kubectl** top
- Query resource allocations with **kubectl** describe
- Browse cluster objects in **Kubernetes** Dashboard
- Add kube-state-**metrics** to your cluster



**Monitor Kube State Metrics on Kubernetes**

1. Monitor node status, node capacity (CPU and memory)
2. Monitor replica-set compliance (desired/available/unavailable/updated status of replicas per deployment)
3. Monitor pod status (waiting, running, ready, etc)
4. Monitor the resource requests and limits.
5. Monitor Job & Cronjob Status
