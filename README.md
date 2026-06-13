# 🌳 Fungal Frontier: Decision Tree Classifier

*A pure Python and NumPy implementation of a binary decision tree classifier to identify edible and poisonous mushrooms.*

![Status](https://img.shields.io/badge/status-active-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Python](https://img.shields.io/badge/python-3.8+-yellow)

This project contains a step-by-step implementation of a binary decision tree classifier from scratch to classify mushrooms as edible or poisonous based on physical attributes. Designed for students, educators, and machine learning enthusiasts, this repository details the core mechanics of decision trees—such as Shannon entropy, binary splitting, information gain, and recursive tree building—without relying on high-level ML frameworks.

---

## 📑 Table of Contents

- [Fungal Frontier: Decision Tree Classifier](#-fungal-frontier-decision-tree-classifier)
  - [Features](#-features)
  - [Technology Stack](#-technology-stack)
  - [Demo and Preview](#-demo-and-preview)
  - [Installation](#-installation)
  - [Usage](#-usage)
  - [Configuration](#-configuration)
  - [Testing](#-testing)
  - [License](#-license)
  - [FAQs](#-faqs)
  - [Contact](#-contact)

---

## ✨ Features

* **Scratch Implementation:** Implements binary decision tree logic without scikit-learn or other high-level machine learning model abstractions.
* **Mathematical Precision:** Features step-by-step implementations of Shannon Entropy, Node-based Dataset Splitting, and Information Gain calculations.
* **Recursive Tree Construction:** Automatically builds decision trees recursively down to a configurable depth limit.
* **Interactive Visualization:** Integrates with NetworkX and Matplotlib to visualize node decisions, subsets, and the final tree topology.
* **Ready-to-Use Dataset:** Pre-configured with a binary-encoded 10-sample mushroom dataset (with cap color, stalk shape, and solitary status features).

---

## 🛠️ Technology Stack

* **Language:** Python 3.8+
* **Numerical Processing:** NumPy
* **Data Visualization:** Matplotlib, NetworkX, Pillow, pydot
* **Development Environment:** Jupyter Notebook / JupyterLab

---

## 📺 Demo and Preview

The decision tree visualizer generates graphical representations showing node splits and indices at each branch. 

For example, when splitting the 10-sample root node on the **Solitary** feature (Feature 2), the dataset splits into:
* **Left branch (Solitary = 1):** Indices `[0, 1, 4, 5, 7]`
* **Right branch (Solitary = 0):** Indices `[2, 3, 6, 8, 9]`

An example visualization of the generated tree layout:

```
 Depth 0, Root: Split on feature: 2
- Depth 1, Left: Split on feature: 0
  -- Left leaf node with indices [0, 1, 4, 7] (Edible)
  -- Right leaf node with indices [5] (Poisonous)
- Depth 1, Right: Split on feature: 1
  -- Left leaf node with indices [8] (Edible)
  -- Right leaf node with indices [2, 3, 6, 9] (Poisonous)
```

> **Note:** To see the graphical nodes featuring mushroom illustrations, please run the Jupyter notebook and check the inline plots.

---

## 🚀 Installation

### Prerequisites

* Python 3.8 or higher.
* Graphviz system-level binary (required for rendering diagrams via `pydot` and `networkx`).
  * **macOS:** `brew install graphviz`
  * **Linux (Ubuntu/Debian):** `sudo apt-get install graphviz`
  * **Windows:** Download and install from [Graphviz Downloads](https://graphviz.org/download/).

### Setup Instructions

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/jayshah-92/decision-tree-classifier.git
   cd decision-tree-classifier
   ```

2. Create a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## 💡 Usage

### Running the Notebook

To explore the code step-by-step and run interactive visualizations, start Jupyter:
```bash
jupyter notebook decision_tree_classifier.ipynb
```
Run through the cells sequentially to observe calculations, run tests, and view tree diagrams.

### Running Programmatically

You can also import and use the decision tree functions in custom Python scripts:

```python
import numpy as np
from decision_tree_classifier import compute_entropy, split_dataset, get_best_split

# One-hot encoded sample data (Brown Cap, Tapering Stalk Shape, Solitary)
X = np.array([[1, 1, 1], [0, 0, 0]])
y = np.array([1, 0])

# Perform split analysis
entropy = compute_entropy(y)
left_idx, right_idx = split_dataset(X, node_indices=[0, 1], feature=0)
best_feat = get_best_split(X, y, node_indices=[0, 1])

print(f"Entropy: {entropy}, Best Splitting Feature Index: {best_feat}")
```

---

## ⚙️ Configuration

Model configurations and properties are defined directly in the notebook:
* **`max_depth`** (default: `2`): The stopping criterion limit. Increasing this depth allows the model to partition data further but might cause overfitting.
* **Feature Names** (configured in `utils.py`):
  * Feature 0: `Brown Cap`
  * Feature 1: `Tapering Stalk Shape`
  * Feature 2: `Solitary`
* **Target Classes**:
  * Label `1`: `Edible`
  * Label `0`: `Poisonous`

---

## 🧪 Testing

The codebase includes a pre-packaged suite of test utilities in [public_tests.py](file:///Users/jayshah/Downloads/jayshah-92/decision-tree-classifier/public_tests.py) to validate your custom implementations.

To execute tests directly from your terminal, run:
```bash
python3 -c "
from public_tests import *
from decision_tree_classifier import compute_entropy, split_dataset, compute_information_gain, get_best_split
import sys

try:
    print('Testing compute_entropy...')
    compute_entropy_test(compute_entropy)
    print('Testing split_dataset...')
    split_dataset_test(split_dataset)
    print('Testing compute_information_gain...')
    compute_information_gain_test(compute_information_gain)
    print('Testing get_best_split...')
    get_best_split_test(get_best_split)
    print('\033[92mAll core algorithms validated successfully!\033[0m')
except AssertionError as e:
    print(f'\033[91mTest failure: {e}\033[0m')
    sys.exit(1)
"
```
---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

## ❓ FAQs

#### **Q: Why am I seeing `pygraphviz` or `pydot` visualization errors?**
**A:** Ensure that the system-level Graphviz binary is correctly installed and added to your system's PATH. See the [Installation](#prerequisites) section for OS-specific commands.

#### **Q: Can I use multi-valued or continuous features in this tree?**
**A:** This specific implementation supports binary features (one-hot encoded values of `0` and `1`). To support continuous features, you would need to extend the `get_best_split` function to search for numerical threshold thresholds.

---

## 📬 Contact

* **Developer:** [Jay Shah](https://github.com/jayshah-92)
* **Medium Article:** [Navigating the Fungal Frontier: Classifying Mushrooms with Decision Trees](https://medium.com/@thejayshah2002/navigating-the-fungal-frontier-classifying-mushrooms-with-decision-trees-c40c08d3abaf)
