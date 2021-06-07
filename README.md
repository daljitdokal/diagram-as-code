# Diagram as code
Diagram as Code allows you to track the architecture diagram changes in any version control system.

## Graphviz
[Graphviz](https://graphviz.org) is open source graph visualization software. Graph visualization is a way of representing structural information as diagrams of abstract graphs and networks. It has important applications in networking, bioinformatics, software engineering, database and web design, machine learning, and in visual interfaces for other technical domains.

The Graphviz layout programs take descriptions of graphs in a simple text language, and make diagrams in useful formats, such as images and SVG for web pages; PDF or Postscript for inclusion in other documents; or display in an interactive graph browser. Graphviz has many useful features for concrete diagrams, such as options for colors, fonts, tabular node layouts, line styles, hyperlinks, and custom shapes.

### Example
![image](https://user-images.githubusercontent.com/7479571/121095516-9189f180-c844-11eb-8a0a-1876a9f76d6b.png)

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

  # git
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
## Graphviz Visual Editor
http://magjac.com/graphviz-visual-editor/
