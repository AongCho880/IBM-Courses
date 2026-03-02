# DBSCAN and HDBSCAN Clustering

### Learning Objectives

After completing this lecture, students should be able to:

* Describe DBSCAN (Density-Based Spatial Clustering of Applications with Noise).
* Explain how DBSCAN works.
* Describe HDBSCAN (Hierarchical Density-Based Spatial Clustering of Applications with Noise).
* Explain how HDBSCAN works and how it differs from DBSCAN.

---

## 1. Introduction to Density-Based Clustering

Density-based clustering identifies **connected regions of high density** in data.

Unlike centroid-based methods (e.g., k-means, hierarchical clustering):

* It does not assume spherical or convex clusters.
* It can detect clusters of arbitrary shape.
* It can identify noise and outliers.

Real-world data often contains:

* Irregular shapes
* Shapes within shapes
* Noise and outliers

Density-based clustering handles these complexities effectively.

---

## 2. DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

### Definition

DBSCAN is a density-based spatial clustering algorithm that creates clusters based on a user-defined density threshold.

It:

* Discovers clusters of any shape, size, or density.
* Distinguishes between cluster points and noise.
* Works well when:

  * The number of clusters is unknown.
  * The dataset contains noise or outliers.

---

## 3. Key Parameters of DBSCAN

DBSCAN requires two parameters:

| Parameter       | Description                                         |
| --------------- | --------------------------------------------------- |
| **ε (epsilon)** | Radius defining the neighborhood                    |
| **MinPts (n)**  | Minimum number of points required in a neighborhood |

These parameters define the density threshold for forming clusters.

---

## 4. Types of Points in DBSCAN

Each data point is classified as one of three types:

### 4.1 Core Point

A point is a **core point** if:

* It has at least **MinPts** points (including itself)
* Within its **epsilon radius**

Core points are focal points of clusters.

---

### 4.2 Border Point

A point is a **border point** if:

* It lies within the neighborhood of a core point
* But does not have enough neighbors to be a core point itself

Border points belong to clusters but are less densely connected.

---

### 4.3 Noise Point

A point is labeled **noise** if:

* It is not within the neighborhood of any core point
* It is isolated from cluster regions

---

## 5. How DBSCAN Works

### Algorithm Steps

1. Select parameters:

   * Epsilon (ε)
   * Minimum points (MinPts)

2. For each point in dataset:

   * Count number of neighbors within ε.
   * Classify as core, border, or noise.

3. Grow clusters:

   * Start from a core point.
   * Include all density-connected neighbors.
   * Expand cluster through connected core points.

4. Unassigned points are labeled as noise.

### Important Property

* DBSCAN is **not iterative**.
* Once points are labeled, clusters are not updated.

---

## 6. DBSCAN Example: Half-Moons Dataset
<p align='conter'>
  <img width="420" alt="image" src="https://github.com/user-attachments/assets/b09a7785-902a-45a5-8252-aad2d20838df" />
  <img width="420" alt="image" src="https://github.com/user-attachments/assets/39740a24-3eef-4672-87bf-9d6fc18416cb" />
  <img width="420" alt="image" src="https://github.com/user-attachments/assets/7575f0c0-6ca7-4c73-84f5-ffbf89c87dda" />
  <img width="420" alt="image" src="https://github.com/user-attachments/assets/6aec441b-0315-43e7-8550-a8a3585f6725" />
</p>


**Figure 1:** DBSCAN applied to noisy half-moons data.

* Blue: Core points
* Orange: Border points
* Black: Noise points

Observation:

* DBSCAN correctly separates curved shapes.
* Noise points remain unlabeled.
* Clusters grow from dense core regions outward.

---

## 7. Strengths of DBSCAN

* Detects clusters of arbitrary shapes.
* Identifies noise explicitly.
* Does not require predefined number of clusters.
* Works well with noisy datasets.

---

## 8. Limitations of DBSCAN

* Requires manual selection of ε and MinPts.
* Sensitive to parameter choices.
* May struggle with varying densities.

---

## 9. HDBSCAN (Hierarchical DBSCAN)

### Definition

HDBSCAN is a variant of DBSCAN that:

* Does not require manual parameter tuning.
* Is less sensitive to noise and outliers.
* Uses **cluster stability** to determine meaningful clusters.

---

## 10. Cluster Stability in HDBSCAN

Cluster stability refers to:

> The persistence of a cluster across a range of density thresholds.

Stable clusters:

* Do not change significantly when neighborhood size varies.
* Are considered more meaningful and robust.

HDBSCAN selects clusters that remain stable over different density levels.

---

## 11. How HDBSCAN Works

HDBSCAN combines:

* Density-based clustering
* Agglomerative hierarchical clustering

### Process Overview

1. Start with each point as its own cluster (initially treated as noise).
2. Gradually lower the density threshold.
3. Agglomerate clusters into a hierarchy.
4. Construct a hierarchical tree.
5. Simplify into a condensed tree.
6. Keep only the most stable clusters.

---

## 12. DBSCAN vs HDBSCAN Example (Canadian Museums Dataset)

Dataset:

* Latitude and longitude of Canadian museums.

### DBSCAN Result

* Found approximately 10 clusters.
* High-density eastern region grouped into one cluster.
* Limited adaptive detail.

### HDBSCAN Result

* Identified more distinct clusters.
* Adaptively adjusted neighborhood sizes.
* Captured varying density regions.
* Produced more coherent clustering.

<img width="1906" height="1054" alt="image" src="https://github.com/user-attachments/assets/0112d8d0-9714-41ec-adb5-0dddaf712016" />

**Figure 2:** Comparison of DBSCAN and HDBSCAN on geographic data.
HDBSCAN provides more adaptive and detailed clustering in dense regions.

---

## 13. Parameter Tuning in Density-Based Methods

By tuning parameters, you can balance:

* Noise mitigation
* Level of detail
* Number of clusters
* Sensitivity to local density variations

HDBSCAN automatically adapts density thresholds, making it more flexible.

---

## 14. Comparison: DBSCAN vs HDBSCAN

| Feature            | DBSCAN                  | HDBSCAN                     |
| ------------------ | ----------------------- | --------------------------- |
| Parameters         | Requires ε and MinPts   | No manual density radius    |
| Noise Handling     | Explicitly labels noise | More robust to noise        |
| Density Adaptation | Fixed density threshold | Adaptive density thresholds |
| Method Type        | Density-based           | Density + Hierarchical      |
| Cluster Selection  | Based on ε              | Based on cluster stability  |

---

## 15. Key Concepts Summary

* DBSCAN is a density-based clustering algorithm.
* It forms clusters from high-density regions.
* Requires two parameters: ε and MinPts.
* Classifies points as core, border, or noise.
* It is not iterative.
* HDBSCAN extends DBSCAN using hierarchical methods.
* HDBSCAN selects clusters based on stability across density levels.
* HDBSCAN is more adaptive and robust to noise.

---

## 16. Key Takeaways

* Density-based clustering is suitable for irregular shapes and noisy data.
* DBSCAN identifies clusters without specifying number of clusters.
* Core, border, and noise point classification is central to DBSCAN.
* DBSCAN may struggle with varying densities.
* HDBSCAN improves flexibility by using hierarchical structure and stability.
* Cluster stability ensures more meaningful cluster selection.

---
