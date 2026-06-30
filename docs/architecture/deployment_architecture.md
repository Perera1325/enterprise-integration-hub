# Deployment Architecture

The Enterprise Integration Hub is designed for a cloud-native Kubernetes deployment.

## Kubernetes Deployment Diagram

```mermaid
graph LR
    User((External Client)) --> Ingress[Nginx Ingress Controller]
    Ingress --> Service[K8s Service: MI]
    
    subgraph K8s Cluster
        Service --> Pod1[MI Pod 1]
        Service --> Pod2[MI Pod 2]
        Service --> PodN[MI Pod N]
        
        Pod1 --> K8sSecrets[K8s Secrets Mount]
        Pod2 --> K8sSecrets
        
        Pod1 -.-> FluentBit[FluentBit DaemonSet]
        Pod2 -.-> FluentBit
    end
    
    FluentBit --> Elasticsearch[(Elasticsearch / Logstash)]
```

## Key Principles
1. **Stateless Nodes**: All WSO2 MI pods are perfectly stateless. Any required state (like caching) is offloaded to a distributed cache (e.g., Redis).
2. **Immutable Infrastructure**: Configuration is baked into the Docker image, parameterized via environment variables injected by Kubernetes Secrets.
3. **Log Aggregation**: MI outputs JSON logs to `stdout`. FluentBit or Promtail running as a DaemonSet captures these logs and forwards them to a centralized observability stack.
