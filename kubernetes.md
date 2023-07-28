# Kubernetes (K8s)

## What is K8s?

- Kubernetes (K8s) is an open-source platform that manages containerized applications.
- It automates deployment, scaling, and management of containers.
- Google developed it, and it's now maintained by CNCF.

![Alt text](imgs/kubernetes-.png)

## Why use and learn K8s?

- Scalability: Easily scale applications based on demand.
- High availability: Ensures applications are always running, even after node failures.
- Portability: Consistently deploy applications across various environments.
- Automation: Automates many tasks, making development and operations smoother.
- Community: Large community and ecosystem support.

## Benefits to business

- Cost-effectiveness: Optimize resource utilization, reducing infrastructure costs.
- Faster time-to-market: Automate deployment for quicker application development.
- Improved reliability: Kubernetes manages application health, enhancing reliability.
- Enhanced collaboration: Promotes DevOps practices for smoother teamwork.
- Competitive advantage: Staying current with Kubernetes keeps businesses competitive.

## What are K8s objects?

- Persistent entities representing the cluster or applications.
- Examples: Pods, Services, Deployments, ConfigMaps, Secrets.
- Each object has a defined specification and interacts with others.
- Managed using Kubectl or Kubernetes API.

![Alt text](imgs/k8.png)

## Concepts of labels and selectors

- Labels: Key-value pairs for identifying and categorizing K8s objects.
- Flexible use: Group objects based on application version, environment, etc.
- Selectors: Used to identify a set of objects based on their labels.
- Commonly used with ReplicationControllers, ReplicaSets, Deployments.
- Important for managing and scaling applications in Kubernetes.
