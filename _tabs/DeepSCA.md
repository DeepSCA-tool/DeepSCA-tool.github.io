---
icon: fas fa-toolbox
order: 1
---

# DeeperBin
DeeperBin is a binary software composition analysis (BSCA) tool designed to detect C/C++ third-party libraries (TPLs) and identify their versions in cross-language invoked C/C++ binaries within polyglot projects, such as those from PyPI and Maven.

## Supported Platforms
- Windows 11
- Python 3.7 or later 
- MongoDB 5.1 or later

## Quick Start
1. Download **DeeperBin**
   
    Download all compressed parts listed on the [**DeeperBin**](https://github.com/DeeperBin/DeeperBin.github.io/tree/main/DeeperBin) page, and extract them to obtain **deeperbin.exe**.
   
    |deeperbin.7z.001|
    | :--: |
    |deeperbin.7z.002|
    |deeperbin.7z.003|
    |deeperbin.7z.004|
    |deeperbin.7z.005|
    |deeperbin.7z.006|

2. Install **DeeperBin**

    Copy **deeperbin.exe** to any directory on your system.

3. Configure MongoDB Database

    - Install MongoDB on your system.
    - Download the [**Feature Database**](https://github.com/DeeperBin/DeeperBin.github.io/blob/main/data/deeperbin-demo-db.7z) of DeeperBin.
  
      `DeeperBin.Feature_Group_Demo.json`: the collection of binary features.
      
      `DeeperBin.PackageMetadata_Demo.json`: the collection of TPL metadata for corresponding binaries.
      
    - Import both collections into your local MongoDB instance (ip: "localhost", port: 27017).

4. Run **DeeperBin**

   Open a command line window in the directory where **deeperbin.exe** is located and run:

    ```
      deeperbin.exe input_file_path output_result_path
    ```

    Replace `input_file_path` with the path to the binary file to be analyzed, and `output_result_path` with the desired output directory.
