---
# the default layout is 'page'
icon: fas fa-file
order: 2
---

## 1. Download Feature Database 

[**Feature Database (JSON)**](https://github.com/DeepSCA-tool/DeepSCA-tool.github.io/blob/main/DeepSCA/feature-db)

## 2. JSON Data Schema

The database adopts a document-based structure, where each document represents the function-level feature vector of a C/C++ third-party library (TPL), including function metadata, file catalogs, and hosting repository information. The detailed field definitions are as follows.

### Function-level Feature Vector

| Field Name | Data Type | Description |
| :--- | :--- | :--- |
| **`sig_full_name`** | String | The function hash, computed via TLSH on normalized code (stripped of whitespace/comments) to support robust matching, excluding functions under 50 characters. |
| **`oss_name`** | String | The name of the C/C++ TPL. |
| **`repo_name`** | String | The name of the hosting repository repository. |
| **`oss_url`** | String | The source URL to the the C/C++ TPL. |
| **`catalog_string`** | String | A space-separated string listing the file catalog of the project (intermediate data). |
| **`sig_info`** | Object | Encoded feature vector data stored in binary format. |
| **`func_feature`** | Object | Encoded function-level feature stored in binary format (intermediate data). |
| **`cluster_label`** | Integer | The label identifier for the project cluster (intermediate data). |
| **`family_label`** | String | The label identifier for the TPL group. |

### An Example of the Function-level Feature Vector

```json
[
  {
    "_id": { "$oid": "64f861ffac66b4cef6cc03f6" },
    "sig_full_name": "nyancat_f20f4e14c25df7873fda535d3188df52",
    "repo_name": "nyancat",
    "oss_name": "nyancat",
    "oss_source": "github",
    "oss_url": "[https://github.com/klange/nyancat](https://github.com/klange/nyancat)",
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
