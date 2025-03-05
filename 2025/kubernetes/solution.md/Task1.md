# **🚀 Understanding Kubernetes Architecture & Deploying a Sample Pod 🚀💡**

## **✨ Scenario**

Familiarize yourself with Kubernetes' control plane and worker node components, then deploy a simple Pod manually.  🎉

---

## **🔹 Steps to Follow**

### **1️⃣ Study Kubernetes Architecture 🏗️**

Kubernetes is composed of **two main Componenets**:

#### **🧠 Control Plane Components (Master Node) 🧩**

These components manage the cluster and handle scheduling, state maintenance, and configuration.

- **API Server**  – The API server on the master node manages API requests, ensuring cluster communication and state validation.
- **Scheduler** – The Scheduler on the master node assigns newly created pods to available nodes based on resource availability and constraints.
- **Controller Manager** – Ensures the desired cluster state matches the actual state.
- **etcd** – The etcd server on the master node stores and manages the cluster's configuration data and state in a highly available key-value store.
- **Cloud Controller Manager** – The Cloud Controller Manager on the master node helps Kubernetes work with cloud services, like managing load balancers and storage in the cloud.

#### **🛠️ Worker Node Components 🔧**

Each worker node runs containers and communicates with the control plane.

- **Kubelet** – The Kubelet ensures containers are running as expected and communicates with the master node to manage pod lifecycle.
- **Container Engine** – The container engine handles container runtime, running containers (e.g., containerd, CRI-O, Docker).
- **Kube Proxy** – Kube proxy manages networking between pods and services and allocates IP addresses to Pods.


---

### **2️⃣ Deploy a Sample Pod 📦**

To deploy a simple NGINX container using Kubernetes, follow these steps:

#### **📝 Create a YAML File (\*\***`pod.yaml`\***\*) **

```yaml                   
apiVersion: v1                # Specifies the API version for the Kubernetes object (v1 is used for basic resources like Pods).
kind: Pod                     # Defines the type of resource, in this case, a Pod. 
metadata:                     # Contains information about the Pod like its name and labels.
  name: nginx-pod             #The name of the Pod.
  labels:                     # Key-value pairs that are used to organize and select resources.
    app: nginx                # A label with key 'app' and value 'nginx' to identify the Pod.
spec:                         #Describes the desired state and configuration of the Pod.
  containers:                 # List of containers to run in this Pod.
    - name: nginx             # The name of the container.
      image: nginx:latest     # The Docker image to use for the container (nginx:latest).
      ports:                  #  Defines the ports that the container will expose.
        - containerPort: 80   # Exposes port 80 inside the container to handle HTTP traffic.
```

**Apply the YAML File**

```bash
kubectl apply -f pod.yaml
```

This command creates an **NGINX pod** inside your Kubernetes cluster.

**Verify the Deployment**

```bash
kubectl get pods
```

If the pod is not running, check its status using:

```bash
kubectl describe pod nginx-pod
```

📌 **NOTE:**

- Make sure **image is available** in the container registry.
- **Map ports correctly** .
- **Make sure YAML syntax is validated** before applying configurations.

---

### **3️⃣. Document Your Learnings **

📌 **Describe Kubernetes Architecture:** Explain the roles of each control plane and worker node component.
📌 **Include your \*\***`pod.yaml`\***\* file:** Clearly explain each section of the YAML and its purpose.
📌 **Things to Take Care Of:** Always verify the **API version in YAML files** as it may change in newer Kubernetes versions! 🔃

---

## **💬 Interview Questions & Answers 📡**

### **1️⃣ How do Kubernetes control plane components work together?**

The **control plane is the brain of Kubernetes**:

- The **API Server** is Frontend interface that processes requests and directs traffic.
- The **Scheduler** Assigns pods to nodes based on resource availability.
- The **Controller Manager** Ensures actual state matches desired state (e.g., node, route, service, volume controllers).
- The **etcd database** stores all cluster state and configurations.
- The **Cloud Controller Manager** integrates cloud services.

Each worker node reports back to the control plane, and **Kubelet ensures that pods are running correctly**. 🚀

### **2️⃣ What is the role of etcd in Kubernetes?**

- etcd is a **distributed key-value store** used by Kubernetes to maintain cluster state.
- It **stores configuration, node status, pod information, and cluster-wide settings**.
- If etcd goes down, the cluster loses its state and cannot function properly. 


### **3️⃣ If a Pod fails to start, how would you diagnose the issue?**

Here are some troubleshooting steps:

🔹 **Check pod status**

```bash
kubectl get pods
```

🔹 **Describe pod details**

```bash
kubectl describe pod <pod-name>
```

🔹 **Check logs for errors**

```bash
kubectl logs <pod-name>
```

🔹 **Inspect events for failures**

```bash
kubectl get events
```

🔹 **Check node status**

```bash
kubectl get nodes
```

💡 **Common Issues & Fixes:**

- ❌ **ImagePullBackOff** – The container image is missing or incorrect. Check image name.
- ❌ **CrashLoopBackOff** – The pod keeps restarting. Check logs for errors.
- ❌ **Pending** – No nodes available. Check `kubectl get nodes` for status.

📌 **NOTE:**

- Verify that **container registry credentials** are correctly configured.
- Check if the pod has **sufficient resources** allocated.
- Ensure **network policies** allow communication if the pod relies on external services.

---

## **🎯 Conclusion 🎉**

You have now learned about Kubernetes architecture and successfully deployed an **NGINX pod!** 


---