# Diagram as code
Diagram as Code allows you to track the architecture diagram changes in any version control system.

### Example
```bash

digraph G {
  # User
  subgraph cluster_user {
    label = "User";
    style=filled;
    color=lightgrey;
    node [style=filled,color=white];

    "Device" [shape=Msquare];
  }

  # Cluster Wrapper
  subgraph cluster_wrapper {
    label = "OC Cluster";
    style=filled;
    color=lightgrey;
    node [style=filled,color=white];

    subgraph cluster_node {
      node [style=filled,color=white];
      label = "Worker Node";
      color=grey;

      subgraph cluster_node {
        node [style=filled];
        label = "Pod";
        color=lightgrey;

        "HashiCorp Vault" [shape=Msquare];
        "8200";
      }
    }
  }
	
  # Connections
  "5002";
  "443";

  # Nexus
  subgraph cluster_nexus {
    style=filled;
    color=lightgrey;
    node [style=filled,color=white];
    label = "Image Registry";
    "vault-image:1.3" [shape=Msquare];
  }

  # gitlab
  subgraph cluster_gitlab {
    style=filled;
    color=lightgrey;
    node [style=filled,color=white];
    label = "Git repo";
    "helm-vault" [shape=Msquare];
  }
	
  # Relationship
  rankdir = LR;
  ranksep="1 equally"
  "Device" -> "443" -> "8200" -> "HashiCorp Vault" [dir=both];
  "HashiCorp Vault" -> "5002" -> "vault-image:1.3" [dir=back];
  "HashiCorp Vault" -> "helm-vault" [dir=back];
}
```
## Graphvix Visual Editor
http://magjac.com/graphviz-visual-editor/
