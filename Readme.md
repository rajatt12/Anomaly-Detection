AI Pipeline for Anomaly Detection in Server Performance Metrics
Student Name: Rajatveer Singh Pasricha
1. Project Overview
This project implements an AI pipeline to detect anomalies in a provided time-series dataset of server performance metrics. The goal is to identify potential incidents by building a robust system that can handle real-world data imperfections, such as missing metrics and unlabeled anomalies.

This project was completed as part of the Round-1 Technical Evaluation for ThoughtData's AI Development Internship, using the provided it_monitoring_dummy_dataset.csv.

2. Problem Understanding & Data Design Strategy
The provided dataset presented two primary challenges:

Challenge 1: Missing Disk Metrics: The assignment required detecting anomalies in disk I/O and utilization, but these metrics were not present in the dataset.
Challenge 2: Unlabeled Data: The dataset did not contain pre-defined anomaly labels.
To overcome these challenges, the following data design strategy was implemented:

Data Augmentation (Simulating Disk Metrics): To meet the project requirements, the missing disk metrics were synthetically generated. It was assumed that disk activity would be correlated with CPU and network activity (e.g., high network traffic might lead to writing data to disk). Therefore, disk_io_read and disk_io_write were simulated based on transformations of the network_in and network_out columns. disk_utilization was simulated with a slow-moving, cyclical pattern. This creative step demonstrates the ability to work with incomplete data.

Unsupervised Anomaly Detection: Since no true anomaly labels were available, two powerful unsupervised models were chosen to identify unusual patterns in the data.

3. AI Models Used
Isolation Forest:

Why I chose it: This model is excellent for identifying outliers in multi-dimensional data. It works by "isolating" anomalies rather than profiling normal data. It is computationally efficient and does not assume a specific distribution of the data, making it ideal for a dataset where the nature of anomalies is unknown.
Autoencoder (Deep Learning):

Why I chose it: An Autoencoder is trained to learn the "normal" behavior of the system. It learns to reconstruct the input data accurately. When an anomalous data point is introduced, the model struggles to reconstruct it, leading to a high "reconstruction error." This method is powerful for detecting subtle deviations from complex patterns that define normal operation.
4. How to Run the Code
The Colab notebook is designed to be run from top to bottom.

Upload the Dataset: The user must upload it_monitoring_dummy_dataset.csv to the Colab environment.
Run All Cells: Go to Runtime -> Run all.
View Results: The final cells will display and save plots showing the server metrics with detected anomalies highlighted.
5. Explainability & Key Observations
The models successfully identified several points as anomalous. Upon visual inspection of the plots, these points often correspond to:

Sudden, sharp spikes or dips in a single metric (e.g., network_in).
Unusual combinations of metrics (e.g., a moment where cpu_usage was high while memory_usage was unusually low).
The final plots provide a clear visual rationale for why a point was flagged, fulfilling the explainability requirement.
