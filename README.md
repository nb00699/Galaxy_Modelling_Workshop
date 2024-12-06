# Gaussian Mixture Model Mock Data and BIC Calculation Using Extreme Deconvolution

This repository contains two notebooks designed for generating and analysing mock datasets in a multidimensional space using Gaussian Mixture Models (GMM) and Extreme Deconvolution (XD) (Bovy et al. 2011). Please cite Buckley et al. 2024 if using.

## Notebook 1: Mock Data Generation
Generates synthetic data using a GMM, introduces observational errors, and saves the dataset to a CSV file.

## Notebook 2: BIC Calculation with Extreme Deconvolution
Calculates the Bayesian Information Criterion (BIC) to determine the optimal number of components in the dataset using Extreme Deconvolution.

## How to Use the Notebooks
### Step 1: `Generating_Mock_Data`
Run the Mock Data Generation notebook first to create a synthetic dataset.
Key Parameters in the Mock Data Notebook:
- num_dimensions: Number of dimensions in the dataset.
- num_components: Number of Gaussian components to generate.
- num_samples: Total number of data points.
- min_separation: Minimum separation between the means of Gaussian components to reduce overlap.
- error_std: Standard deviation of the Gaussian errors added to the data.
Output: A CSV file named `generated_data_with_errors.csv`

### Step 2: `Calculating_the_BIC_for_Mock_Data_Using_XD`
Run the BIC Calculation with Extreme Deconvolution notebook to analyse the dataset.
- Reads in the `generated_data_with_errors.csv` file.
Output: Visualises the BIC scores to help identify the optimal number of components.

## Potential Issues and Solutions
### Instability in Extreme Deconvolution (XD)
Due to the nature of mock data generation, the XD algorithm may struggle to converge in some cases. This can result in:
- Warnings about "log-likelihood decreasing."
- Errors or nonsensical results in the BIC scores.
  
#### Common Causes:
- Poorly conditioned covariance matrices: If the covariance matrices generated for the Gaussian components are near-singular or improperly scaled, XD may fail.
- High dimensionality: XD becomes unstable with increasing dimensions or poorly separated components.
- Scaling issues: If the errors or data are not scaled correctly, XD can behave unpredictably.
  
#### Solutions:
- Regularisation: Ensure covariance matrices are regularised to avoid numerical instability.
- Dimensionality Reduction with PCA (`https://scikit-learn.org/1.5/modules/generated/sklearn.decomposition.PCA.html`): Applying Principal Component Analysis (PCA) to restructure the dataset can improve the performance of XD.
