This project was developed as part of an academic assignment. It demonstrates a comprehensive, hands-on implementation of Role-Based Access Control (RBAC) in a Kubernetes cluster using Minikube. RBAC is a fundamental security practice that enforces strict access control based on user roles.

## 📚**Key Concepts**

* 🔐 **RBAC (Role-Based Access Control) in Kubernetes:** Understand how to enforce security policies that limit what users can see or do inside a Kubernetes cluster.

* 🧑‍💻 **User Management via Certificates:** Learn how Kubernetes handles authentication through certificate-based identities instead of traditional usernames and passwords.

* 📄 **Custom kubeconfig Files:** Explore how to generate and use customized kubeconfig files that define users, clusters, and contexts—critical for managing multiple users securely.

* 🛡️ **Role & RoleBinding:** Gain practical experience creating fine-grained access controls within a specific namespace by assigning specific verbs (actions) on resources.

* 🌐 **ClusterRole & ClusterRoleBinding:** Elevate permissions beyond a single namespace, enabling users to operate across the entire cluster—great for admin or DevOps tasks.

* 🧪 **Testing Access Control:** Learn how to verify access, check for expected failures (like forbidden errors), and debug user permissions.

* 📂 **Namespace Isolation:** Understand why separating workloads across namespaces enhances security and structure in real-world deployments.

## 🛠 Task Breakdown
### 🧱 Task 1: Minikube Setup & NGINX Deployment

* Initialized Minikube to simulate a Kubernetes cluster locally

* Created a dedicated namespace cy5130-rbac to isolate access

* Deployed an NGINX application (ananya-nginx1) in that namespace to test RBAC rules later

🔍 Relevance: Namespaces help enforce security by isolating resources. This task prepares the environment to validate access control.

### 👤 Task 2: Creating Kubernetes Users

* Discovered the cluster’s Certificate Authority (CA) files

* Created new users (e.g., Ananya) by generating private keys, CSRs, and certs

* Built a new kubeconfig file (cy5130.config) to authenticate as the new user

🔍 Relevance: Kubernetes doesn't have traditional users. Instead, authentication is done via certificates. This task shows how secure identities are created in Kubernetes clusters.

### 🧾 Task 3: Roles and RoleBindings

* Attempted to list pods with the new user (expectedly failed)

* Created a Role named ananya-pods that allows get, watch, list, create, and delete on pods and deployments

* Bound the Role to Ananya via a RoleBinding (ananya-rb)

* Verified scoped access to namespace cy5130-rbac

* Deployed another NGINX app (ananya-nginx2) and deleted the original one

🔍 Relevance: Role and RoleBinding ensure least privilege access. This task proves how to enforce namespace-scoped permissions.

### 👥 Task 3.2: Adding a Second User

* Created another user (Ananya2) with a separate private key, certificate, and kubeconfig entry

* Added a new context cy5130-2 linked to this user in cy5130.config

* Verified that the new user (Ananya2) had no default permissions (access denied)

* Created a Role named ananya2-pods to allow only listing pods

* Created a RoleBinding named ananya2-rb to bind the new user to this minimal Role

🔍 Relevance: This showcases the granular permission model of Kubernetes, allowing each user to have precise access based on need.


### 🌐 Task 4: ClusterRoles and ClusterRoleBindings

* Created a ClusterRole named ananya-cr that allowed pod and deployment operations across all namespaces

* Created a ClusterRoleBinding named ananya-crb to bind this role to the user Ananya

* Verified that Ananya could deploy resources like ananya-nginx3 to the default namespace without switching contexts

🔍 Relevance: Demonstrates how cluster-wide permissions can be managed efficiently using ClusterRoles and bindings.

### 🔧 Technologies Used

* Minikube 🐳 — Local Kubernetes environment

* kubectl 📦 — Kubernetes CLI tool

* OpenSSL 🔑 — For certificate creation

### 🔐 Core Security Concepts Demonstrated

* Role-Based Access Control (RBAC)

* Certificate-based user authentication

* Context switching with kubeconfig

* Namespace isolation and privilege restriction


