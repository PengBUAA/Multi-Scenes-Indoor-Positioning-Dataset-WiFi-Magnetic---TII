# Multi-Scenes Indoor Positioning Dataset (WiFi & Magnetic Field)

This repository contains a comprehensive indoor positioning dataset collected from two distinct real-world scenarios: a standard university teaching building and a large-scale international airport. The dataset integrates **WiFi Fingerprinting (RSSI)** and **Magnetic Field Strength** to support research in multi-source fusion, fingerprint database compression, and lightweight localization algorithms.

## 1. Scenario Descriptions

### Scenario A: BUAA Teaching Building
* **Characteristics**: Regular spatial structure with relatively stable electromagnetic environments.
* **Data Format**: **Dense Matrix Representation**. WiFi signals are organized in a traditional "flat" structure where each unique MAC address represents a single dimension.
* **Best For**: Baseline algorithm verification and basic deep learning model training (e.g., CNN, MLP).

### Scenario B: Guiyang Longdongbao International Airport
* **Characteristics**: Large-scale open space with an extremely high density of Access Points (APs).
* **Data Format**: **Sparse Key-Value Representation**. Due to the massive number of MAC addresses, a traditional dense matrix would be memory-inefficient. Instead, data is organized via `GroupID`.
* **Implementation**: Each location coordinate is mapped to a specific `GroupID`, which stores only the detected `[MAC Address, RSSI]` pairs at that point, significantly reducing storage overhead.

---

## 2. Dataset Structure

The dataset for each scenario includes the following core variables:

| Variable | Shape/Type | Description |
| :--- | :--- | :--- |
| `Postrain` | $N \times 3$ Matrix | Position ID and Training set reference coordinates (id, x, y) |
| `Postest` | $M \times 3$ Matrix | Position ID and Test set ground truth coordinates (id, x, y) |
| `RSStrain` | Matrix | Training set WiFi RSSI fingerprints |
| `RSStest` | List | Test set WiFi RSSI fingerprints |
| `Magtrain` | $N \times 3$ Matrix | Training set Tri-axial magnetic field strength |
| `Magtest` | $M \times 3$ Matrix | Test set Tri-axial magnetic field strength |



### Note on Airport Data Mapping
To handle the high-dimensional nature of the airport environment, users should:
1. Locate the `GroupID` corresponding to the target row in `Postrain`/`Postest`.
2. Retrieve the active MAC addresses and their corresponding RSSI values from the fingerprint library using the `GroupID` index.

---

## 3. Usage & Requirements

* **File Format**:  `.csv` 
* **Recommended Environment**: Python 3.8+ or MATLAB 2022b+
* **Key Dependencies**: `numpy`, `pandas`, `scipy`

---

## 4. Contact

For any questions regarding the dataset, please feel free to contact:
* **Email**: [zhanpeng_zhang@buaa.edu.cn]
* **Affiliation**: [Beihang University]
