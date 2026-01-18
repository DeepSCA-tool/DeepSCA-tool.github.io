---
# the default layout is 'page'
icon: fas fa-info-circle
order: 3
---

# Ground-truth Dataset

This Ground-truth Dataset provides a comprehensive view of software dependency graphs. The core data is provided in **JSON format**, capturing the intricate topological structures of project dependencies in detail. It provides standardized data support for in-depth research into the relationships between components.

## 1. Dataset Download

* **Dependency Graph View (JSON)**:
    [**Download Ground-truth Dataset (JSON)**](https://github.com/DeepSCA-tool/DeepSCA-tool.github.io/blob/main/data/ground_truth_dataset.zip)

---

## 2. JSON Data Schema

The dataset adopts a hierarchical structure, where each entry represents a **Self-Developed Project**. It details the direct usage of **Third-Party Libraries (TPLs)** by the project and recursively demonstrates the transitive dependencies between these TPLs.

### 2.1 Root Object (Project Level)

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`self_developed_project`** | String | The unique identifier or name of the host project (self-developed project). |
| **`third_party_libraries`** | List | A list of all third-party libraries involved in the project's dependency tree (including both direct and indirect dependencies). |
| **`dependency_graph`** | List | A list of edges defining the topology of the dependency graph (see **2.3**). |

### 2.2 Third-Party Library List (`third_party_libraries`)

Classifies and defines the libraries found within the dependency tree.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`name`** | String | The name of the third-party library (e.g., `openssl`, `musl`). |
| **`dependency_type`** | String | **`direct`**: Libraries explicitly imported or included by the self-developed project.<br>**`indirect`**: Libraries introduced transitively via other TPLs. |

### 2.3 Graph Edges (`dependency_graph`)

Defines the specific directional relationships ("edges") in the graph.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`source_project`** | String | **Caller (Upstream)**. Can be the self-developed project or a TPL. |
| **`target_project`** | String | **Callee (Downstream)**. The target library being depended upon. |
| **`relation_type`** | String | **`direct_usage`**: Self-Developed Project → TPL.<br>**`transitive_dependency`**: TPL → TPL (Transitive Dependency). |
| **`file_evidence`** | List | A list of specific file pairs proving the existence of this dependency (source-code level evidence). |

### 2.4 File Evidence (`file_evidence`)

Provides ground-truth evidence at the file level.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`source`** | String | The path of the source file initiating the import/include. |
| **`target`** | String | The path of the target file being referenced. |

### 2.5 Data Example

```json
[
  {
    "self_developed_project": "ability_ability_base",
    "third_party_libraries": [
      {
        "name": "third_party_mesa3d",
        "dependency_type": "direct"
      },
      {
        "name": "third_party_bounds_checking_function",
        "dependency_type": "direct"
      },
      {
        "name": "third_party_json",
        "dependency_type": "direct"
      },
      {
        "name": "third_party_musl",
        "dependency_type": "indirect"
      }
    ],
    "dependency_graph": [
      {
        "source_project": "ability_ability_base",
        "target_project": "third_party_mesa3d",
        "relation_type": "direct_usage",
        "file_evidence": [
          {
            "source": "foundation/ability/ability_base/test/unittest/want/array_wrapper_test.cpp",
            "target": "third_party/mesa3d/src/gtest/include/gtest/gtest.h"
          },
          {
            "source": "foundation/ability/ability_base/test/unittest/cwant/capi_want_test.cpp",
            "target": "third_party/mesa3d/src/gtest/include/gtest/gtest.h"
          }
        ]
      }
    ]
  }
]
```