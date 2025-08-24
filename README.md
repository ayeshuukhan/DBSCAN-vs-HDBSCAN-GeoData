## Project Overview

This project demonstrates:

* How to apply **DBSCAN** and **HDBSCAN** for clustering geospatial data.
* How to visualize clusters on a map using **GeoPandas** and **Basemap**.
* How density variations affect clustering results.

The dataset contains facility locations in Canada, including **latitude** and **longitude** coordinates.

---

## Dataset

The dataset includes the following columns:

* `Facility_Name` – Name of the facility
* `Source_Facility_Type` – Type of the source facility
* `Provider` – Service provider name
* `City`, `Prov_Terr`, `Postal_Code` – Address details
* `Latitude`, `Longitude` – Geographic coordinates
* … and other address-related details

---

## How to Run

1. Load the dataset.

2. Run DBSCAN for clustering:

   ```python
   dbscan = DBSCAN(eps=1.0, min_samples=3, metric='euclidean').fit(coords_scaled)
   df['Cluster'] = dbscan.fit_predict(coords_scaled)
   ```

3. Run HDBSCAN for clustering:

   ```python
   hdbscan = HDBSCAN(min_cluster_size=5).fit(coords_scaled)
   df['Cluster_HDBSCAN'] = hdbscan.labels_
   ```

4. Visualize the clusters on a map:

   ```python
   plot_clustered_locations(df, title='Clustered Locations')
   ```

---

## Visualization

* DBSCAN clusters based on density and proximity.
* HDBSCAN automatically handles varying densities and identifies noise better.

---

## Comparing DBSCAN vs HDBSCAN

| Feature          | DBSCAN               | HDBSCAN               |
| ---------------- | -------------------- | --------------------- |
| Density Handling | Single density       | Varying densities     |
| Noise Detection  | Yes                  | Yes (Better handling) |
| Parameters       | `eps`, `min_samples` | `min_cluster_size`    |
| Cluster Shape    | Arbitrary            | Arbitrary             |

---

## 📌 Use Cases

* **Urban Planning**: Identify regions with dense facility coverage.
* **Logistics**: Detect areas underserved by facilities.
* **Public Health**: Find clusters of medical centers for resource allocation.
