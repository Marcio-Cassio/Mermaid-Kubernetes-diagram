```mermaid
flowchart TB
    subgraph Cluster ["Kubernetes cluster"]
        subgraph ControlPlane ["Control plane node"]
            apiserver["kube-apiserver"]
        end

        subgraph Worker1 ["Worker node 1"]
            pod1["Pod: app"]
        end

        subgraph Worker2 ["Worker node 2"]
            pod2["Pod: app"]
        end

        subgraph Worker3 ["Worker node 3"]
            pod3["Pod: app"]
        end

        ingress["Ingress controller"]
        service["Service"]
    end

    computer["Your computer(kubectl)"]
    internet["Internet(HTTP request)"]
    external["External API / database(outside the cluster)"]

    %% Connections
    computer -- "kubectl apply" --> apiserver
    internet -- "HTTP" --> ingress
    ingress --> service
    
    service --> pod1
    service --> pod2
    service --> pod3

    apiserver -- "schedules pods" --> pod1
    apiserver -- "schedules pods" --> pod2
    apiserver -- "schedules pods" --> pod3

    pod1 -- "queries" --> external
    pod2 -- "queries" --> external
    pod3 -- "queries" --> external
...