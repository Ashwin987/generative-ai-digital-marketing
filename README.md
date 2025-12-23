Predictive & Generative AI for Digital Marketing Data

STAT414 Final Report University of California, Los Angeles (UCLA) March 23, 2025

Authors

    Hochan Son 

Stephanie Lu

Ashwin Ramaseshan

Juyi Yang

Project Overview

This study investigates the effectiveness of five state-of-the-art synthetic data generation approaches for digital marketing applications. The research specifically addresses persistent challenges in marketing data, including:

    Extreme Class Imbalance: Positive click events often represent less than 2% of observations.

Privacy Restrictions: Limitations on data sharing and regulatory compliance (GDPR/CCPA).

Data Scarcity: The high cost of obtaining labeled examples for model training.

The goal was to generate high-quality synthetic data that maintains the statistical properties of real data while improving the predictive utility of machine learning models.

Methodology & Models

The study evaluates five distinct approaches for tabular data synthesis:

    CTGAN (Conditional Tabular GAN): Simultaneously trains a generator and discriminator specifically for mixed categorical and continuous tabular features.

TVAE (Tabular Variational Autoencoder): Uses variational inference to encode relationships between features into a lower-dimensional latent space.

TG-GPT2 (Tabular Generator-GPT2): A fine-tuned transformer-based framework that uses a specialized tokenization strategy to represent tabular structures (rows, columns, and data types).

TabDDPM: A diffusion-based model that iteratively denoises data to mirror real distributions.

SMOTE: A traditional interpolation technique used as a baseline for minority class oversampling.

Dataset Description

    Source: Digital marketing ad click dataset.

Size: 7 million records (sampled to 10% for computational efficiency).

Features: 35 features covering user demographics, device information, contextual data, and ad attributes.

Imbalance Ratio: Extreme 99:1 ratio of non-clicks to clicks.

Evaluation Metrics

Models were assessed using two primary dimensions:

    Fidelity: Measured via Jensen-Shannon (JS) Divergence and Kolmogorov-Smirnov (KS) Statistics to see how closely synthetic data matches the original distribution.

Utility: Evaluated by training XGBoost and CatBoost models on synthetic data and testing them on real data using Accuracy, Precision, F1-Score, and ROC AUC.

Key Results

CTGAN emerged as the definitive leader in the evaluation:

Method	Fidelity Score	Utility Score	Combined Score
CTGAN	0.9998	1.0000	0.9999
TG-GPT2	0.9625	0.9999	0.9812
TVAE	0.8559	0.9999	0.9279
SMOTE	0.8457	0.9958	0.9208

    CTGAN achieved near-perfect statistical similarity and superior ROC AUC scores (0.9714/0.9081), indicating exceptional classification performance.

TG-GPT2 showed high fidelity but required significant computational resources, processing only 6-7 tokens per second on standard hardware.

GPT-2 (Base) showed reasonable fidelity but catastrophically poor utility, highlighting that statistical similarity alone does not guarantee model performance.

Implementation Details

    Pre-processing: Includes one-hot encoding for low-cardinality features and target encoding for high-cardinality features.

Environment: The implementation was containerized using Docker to ensure reproducibility and resolve library compatibility issues.

Hardware Considerations: TG-GPT2 training parameters were dynamically adjusted for GPU vs. CPU environments.
