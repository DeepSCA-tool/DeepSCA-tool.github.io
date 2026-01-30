---
# the default layout is 'page'
icon: fas fa-info-circle
order: 3
---

## 1. Download Ground-truth Dataset 

We constructed a new ground-truth dataset because existing public datasets lack dependency graph annotations, and the dataset from recent dependency studies is not publicly available.

[**Ground-truth Dataset (JSON)**](https://github.com/DeepSCA-tool/DeepSCA-tool.github.io/blob/main/data/ground_truth_dataset.zip)
    
## 2. JSON Data Schema

The dataset adopts a hierarchical structure, where each item represents a **C/C++ Project**. It details all reused **C/C++ TPLs** and their **inter-TPL dependency graph**.

### C/C++ Project Object

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`self_developed_project`** | String | The name of the C/C++ project. |
| **`third_party_libraries`** | List | A list of all C/C++ TPLs reused in the C/C++ project (including both direct and transitive reused TPLs). |
| **`dependency_graph`** | List | A list of edges(dependency relations) of the dependency graph. |

### Reused C/C++ TPL List

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`name`** | String | The name of the C/C++ TPLs (e.g., `openssl`, `musl`). |
| **`dependency_type`** | String | **`Direct`**: C/C++ TPLs explicitly imported or included by the C/C++ project.<br>**`Transitive`**: C/C++ TPLs introduced transitively via other TPLs. |

### TPL-level Dependency List (Inter-TPL Dependency Graph)

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`source_project`** | String | **Caller**. Can be the C/C++ project or TPL. |
| **`target_project`** | String | **Callee**. The C/C++ TPL reused by the C/C++ project or other TPL. |
| **`relation_type`** | String | **`direct_usage`**: Project/TPL → TPL (Direct Dependency). <br> **`transitive_dependency`**: TPL → TPL (Transitive Dependency). |
| **`file_evidence`** | List | A list of specific file pairs proving the existence of this dependency (file-level dependency). |

### File-level Dependnecy List

Provides ground-truth evidence at the file level.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`source`** | String | The path of the source file initiating the import/include. |
| **`target`** | String | The path of the target file being referenced. |

### An Example of the C/C++ Project Object

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
        "target_project": "third_party_bounds_checking_function",
        "relation_type": "direct_usage",
        "file_evidence": [
          {
            "source": "foundation/ability/ability_base/interfaces/kits/c/cwant/src/want.cpp",
            "target": "third_party/bounds_checking_function/include/securec.h"
          },
          {
            "source": "foundation/ability/ability_base/interfaces/kits/native/extractortool/src/extractor.cpp",
            "target": "third_party/bounds_checking_function/include/securec.h"
          },
          {
            "source": "foundation/ability/ability_base/interfaces/kits/native/extractortool/src/zip_file.cpp",
            "target": "third_party/bounds_checking_function/include/securec.h"
          }
        ]
      }
    ]
  }
]

```


