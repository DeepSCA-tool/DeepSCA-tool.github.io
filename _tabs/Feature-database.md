---
# the default layout is 'page'
icon: fas fa-file
order: 2
---

# Feature Database (feature-db)

## 1. Dataset Download

* **Feature Database (JSON)**:
  [**Download Feature-db Dataset (JSON)**](https://github.com/DeepSCA-tool/DeepSCA-tool.github.io/blob/main/DeepSCA/feature-db)

---

## 2. JSON Data Schema

The dataset adopts a document-based structure, where each entry represents a specific version or signature instance of an **OSS Project**. It details metadata, file catalogs, modification ratios, and encoded binary feature vectors.

### 2.1 Root Object (Project Feature Level)

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`sig_full_name`** | String | The unique identifier for this signature instance (e.g., `nyancat_f20f...`). |
| **`oss_name`** | String | The common name of the Open Source Software (e.g., `nyancat`). |
| **`repo_name`** | String | The specific repository name. |
| **`oss_source`** | String | The source platform of the software (e.g., `github`). |
| **`oss_url`** | String | The URL to the source code repository. |
| **`catalog_string`** | String | A space-separated string listing the file structure/catalog of the project. |
| **`sig_info`** | Object | Encoded signature data stored in binary format (see **2.3**). |
| **`func_feature`** | Object | Encoded function-level feature data stored in binary format (see **2.3**). |
| **`modify_ratio`** | Object | A dictionary recording modification statistics for specific files (see **2.2**). |
| **`cluster_label`** | Integer | The label identifier for the project cluster. |
| **`family_label`** | String | The label identifier for the software family. |

### 2.2 Modification Statistics (`modify_ratio`)

Records the change history and ratio for files within the project. The key is the file path.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`changes`** | Integer | The number of changes detected. |
| **`start_time`** | String | The timestamp of the first recorded change. |
| **`end_time`** | String | The timestamp of the last recorded change. |
| **`ratio`** | Float | The calculated modification ratio (e.g., `0.00097`). |

### 2.3 Binary Feature Data (`sig_info` / `func_feature`)

Stores high-dimensional feature vectors or signature hashes using MongoDB Binary format (`$binary`).

| Field Name | Type | Description |
| :--- | :--- | :--- |
| **`base64`** | String | The Base64 encoded string of the binary feature data. |
| **`subType`** | String | The binary subtype identifier (e.g., `"00"`). |

### 2.4 Data Example

```json
[
  {
    "_id": { "$oid": "64f861ffac66b4cef6cc03f6" },
    "sig_full_name": "nyancat_f20f4e14c25df7873fda535d3188df52",
    "repo_name": "nyancat",
    "oss_name": "nyancat",
    "oss_source": "github",
    "oss_url": "[https://github.com/klange/nyancat](https://github.com/klange/nyancat)",
    "src_local_path": "open-harmony\\oss_dataset_repos\\nyancat_f20f4e14c25df7873fda535d3188df52",
    "sig_info": {
      "$binary": {
        "base64": "H4sIAHFoRWYC/6WSvW5TQRCFkQISwnkQKmv+dnem3J/ZB+ANIHFkSxYpYncUNHSWiMTlfRmTIOKCim1mda/0nTPn7NfXP79cvfp9Tqub+/1+c3PY3X9+WE6r283dx+P+cLu7OSw/ltPbT8fd/rA7/7p62Jw/fVs+LO9PMxWHMXOTicmJek+GyEw1QwUC9Ybm1AjZsiVhLBlmZQBRNm9lttxsLN+D9QbXaU3L08TnCcvjaY7UAElBAUwzQSbChqoCUHA4MCDrQOpG3Iugc3LAFhLA3Yvm1hH6WWT7brvaXgdS4YwcAZMsDTpzmmAyelyHBbp3mwCAUKnE6MAO1qxLEUuhSIJJL5DUJhJbqHvFLq36LN2GU+7cc5hVy41BKiVATzQhtVlaEikMmWeulqw+IQMXamCxqxCEewCl2SMCBu3sWkQhlwgzvAn0USTzyLGpQQQf+SYqk0a7cFjdQWbvjDTTkGrigZcmxJlGyDP1iBm5ljamp8xuUor0oWBAkysmvFxaygBzLjit2hT36mhhJ4UpCZ+QsCrmKqIIPsLZILQhOXdVYqc+IoALJFusZGOShlig1WBqi3zAizGhx5m1ACOkAjayRYugCoM9BBuLKdpl2+O5mhLv8WU16V/V5HM1+Kea8rea1TnH+X+4F01fPx7XvwCxZx8PhwMAAA==",
        "subType": "00"
      }
    },
    "sig_info_cnt": 10,
    "ver_cnt": 3,
    "catalog_string": "CHANGELOG Makefile nyancat.1 README.md src\\animation.c src\\Makefile src\\nyancat.c src\\telnet.h systemd\\nyancat.socket systemd\\nyancat@.service",
    "cluster_label": 2443,
    "metafile": [ "README.md" ],
    "modify_ratio": {
      "src/nyancat.c": {
        "file": "src/nyancat.c",
        "changes": 1,
        "start_time": "2015-10-31 14:51:33",
        "end_time": "2018-08-18 22:40:20",
        "days": 1022,
        "ratio": 0.0009784735812133072
      }
    },
    "func_feature": {
      "$binary": {
        "base64": "H4sIAN1sZmYC/6WSO25UQRBFkQwS8rAQolH9ursq7E/1AtgB+COPNMKBZzICErKRsMRjv9QzRngCIjqp1nvSubfu7a+vf365ePV0Tpur+/3+5uqwu//8sJw21ze3H4/7w/Xu6rD8WE5vPx13+8Nu/XXxcLN++rZ8WN6fZioOY+YmE5MT9Z4MkZlqhgoE6g3NqRGyZUvCWDLMygCibN7KbLnZWL4H6w1u0xaW3xOfJy2PpzlSAyQFBTDNBJkIG6oKQMHhwICsA6kbcS+CzskBW0gAdy+aW0foq8jd5d3m7l0gFVbkCJhkadCZ0wST0eM6LNC92wQAhEolRgd2sGZdilgKRRJMeoakNpHYQt0rdmnVZ+k2nHLnnsOsWm4MUikBeqIJqc3SkkhhyDxztWT1CbniQg0sdhWCcA+gNHtEwKCdXYso5BJhhjeBPopkHjk2NYjgI99EZdJoZw6rO8jsnZFmGlJNPPDShDjTCHmmHjEj19LG9JTZTUqRPhQMaHLFhOdLSxlgzgWnVZviXh0t7KQwJeETElbFXEUUwUc4G4Q2JOeuSuzURwRwhmSLlWxM0hALtBpMbZEPeDEm9DizFmCEVMBGtmgRVGGwh2BjMUU7b3s8V1PiPb6sJv2rmrxWg3+qKX+r2aw5zv/DvWj68vG4/QVQSfSThwMAAA==",
        "subType": "00"
      }
    },
    "func_feature_cnt": 10,
    "family_label": "1295"
  }
]
```