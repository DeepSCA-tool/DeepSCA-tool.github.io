---
icon: fas fa-toolbox
order: 1
---

DeepSCA is a software composition analysis (SCA) tool for C/C++ source-code projects, designed to detect reused C/C++ third-party libraries (TPLs) and recovery the inter-TPL dependency graph.

## Supported Platforms
- Python 3.9 or later
- MongoDB 5.1 or later

## Quick Start

### 1. Download DeepSCA
Download the latest **DeepSCA** compressed package and extract it:
* [**DeepSCA v2.0**](https://github.com/DeepSCA-tool/DeepSCA-tool.github.io/blob/main/DeepSCA/deepsca-2.0.zip)

### 2. Configure Environment & Database
Before running DeepSCA, you need to set up the MongoDB database and update the tool's configuration file (`config.yml`).

1.  **Install MongoDB**: Ensure MongoDB is installed and running on your system (Version 5.1+ is recommended).
2.  **Import Data**:
    * Download the feature database package.
    * Import **`deepsca-feature-db`** into your local MongoDB instance.
3.  **Configure `config.yml`**:
    * Locate the `config.yml` file in the extracted DeepSCA directory.
    * Edit the file to include your MongoDB connection details (IP, Port, Database Name) to ensure DeepSCA can access the feature data.

### 3. Run DeepSCA
**DeepSCA** is a Python-based tool with `detector.py` serving as the main entry point.

1.  Open a Command Line or Terminal window.
2.  Navigate to the directory containing `detector.py`.
3.  Run the analysis using the following command structure:

    ```bash
    python detector.py -i <source_directory> -o <result_directory>
    ```

    **Parameters:**
    * `-i` or `--source_dir`: Path to the directory containing the project binaries/source code you wish to analyze.
    * `-o` or `--result_dir`: Path to the directory where the output results (`.jl` files) will be saved.

    **Example:**
    ```bash
    python detector.py -i ./data/targets -o ./results
    ```

    **Optional Arguments:**
    You can also adjust the number of worker processes or detection thresholds:
    ```bash
    # Run with 8 worker processes
    python detector.py -i ./data/targets -o ./results -w 8
    ```
    

    *(For a full list of options, run `python detector.py --help`)*

