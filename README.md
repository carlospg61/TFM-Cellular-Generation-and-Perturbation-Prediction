# TFM-Cellular-Generation-and-Perturbation-Prediction
Master's Thesis (TFM) project focusing on the generation of synthetic single-cell RNA-seq profiles and the prediction of cellular responses to perturbations using Autoencoders and Conditional Latent Diffusion Models.

## Project Overview

Analyzing single-cell RNA sequencing (scRNA-seq) data is challenging due to high dimensionality and biological noise. This project overcomes these challenges by compressing gene expression data (2000 highly variable genes) into a lower-dimensional latent space using a custom **Autoencoder**. Once in the latent space, **Diffusion Models** are applied to:
1. Generate realistic synthetic cells of specific lineages (B cells, T cells, Dendritic, etc.).
2. Predict how a cell's gene expression profile shifts when exposed to a biological perturbation (e.g., transition from a *control* state to a *stimulated* state).

## Repository Structure & Methodology

The project is divided into two main computational pipelines:

### 1. Synthetic Cell Generation (`Generacion_celulas.ipynb`)
* **Autoencoder Architecture:** A custom neural network that compresses the 2000-gene expression matrix into a 128D latent space representation (similar in concept to *Scimilarity*). 
* **Classifier-Guided Diffusion:** A denoising diffusion probabilistic model trained on the latent space. A custom classifier network provides gradient guidance during the reverse diffusion process, steering the model to generate specific synthetic cell types (e.g., CD4+ T, CD14+ Monocytes, NK cells).
* **Validation:** UMAP dimensionality reduction is used to visually validate that the synthetic cells cluster perfectly with their real-world biological counterparts.

### 2. Perturbation Prediction (`Prediccion_perturbaciones.ipynb`)
* **Conditional Latent Diffusion:** A separate diffusion model conditioned on both *Cell Type* and *Biological State/Condition*. 
* **State Transition (Guidance):** The model simulates the perturbation effect (e.g., stimulation). By manipulating the conditioning labels during the denoising steps, we mathematically "push" a control cell latent vector toward the stimulated state.
* **Decoding & Evaluation:** The perturbed latent vectors are passed through the frozen Autoencoder's decoder to retrieve the new 2000-gene profiles. 
* **"Judge" Classifier:** A Random Forest classifier, acting as a biological judge, is trained on real data to quantitatively evaluate whether the synthetically perturbed cells genuinely exhibit the features of true stimulated cells.

## Tech Stack & Libraries

* **Deep Learning:** PyTorch (`torch`, `torch.nn`, `torch.optim`)

----------------------------------------------------------------------------------------------------------------------------------------------------------------

## Descripción General del Proyecto

El análisis de datos de secuenciación de ARN de célula única (scRNA-seq) representa un gran desafío debido a su alta dimensionalidad y al ruido biológico inherente. Este proyecto supera estos obstáculos comprimiendo los datos de expresión génica (2000 genes altamente variables) en un espacio latente de menor dimensión utilizando un **Autoencoder** personalizado. Una vez en el espacio latente, se aplican **Modelos de Difusión** para:

1. Generar células sintéticas realistas de linajes específicos (células B, células T, Dendríticas, etc.).
2. Predecir cómo cambia el perfil de expresión génica de una célula cuando se expone a una perturbación biológica (por ejemplo, la transición de un estado de *control* a un estado *estimulado*).

## Estructura del Repositorio y Metodología

El proyecto se divide en dos flujos de trabajo (pipelines) computacionales principales:

### 1. Generación de Células Sintéticas (`Generacion_celulas.ipynb`)
* **Arquitectura del Autoencoder:** Una red neuronal personalizada que comprime la matriz de expresión de 2000 genes en una representación de espacio latente de 128 dimensiones (similar en concepto a *Scimilarity*). 
* **Difusión Guiada por Clasificador:** Un modelo probabilístico de difusión de eliminación de ruido (*denoising*) entrenado en el espacio latente. Una red clasificadora personalizada proporciona una guía de gradiente durante el proceso de difusión inversa, dirigiendo al modelo para generar tipos de células sintéticas específicas (ej. linfocitos T CD4+, monocitos CD14+, células NK).
* **Validación:** Se utiliza la reducción de dimensionalidad UMAP para validar visualmente que las células sintéticas se agrupan (clusterizan) perfectamente con sus homólogas biológicas del mundo real.

### 2. Predicción de Perturbaciones (`Prediccion_perturbaciones.ipynb`)
* **Difusión Latente Condicional:** Un modelo de difusión independiente condicionado tanto por el *Tipo Celular* como por el *Estado/Condición Biológica*. 
* **Transición de Estado (Guidance):** El modelo simula el efecto de la perturbación (ej. estimulación). Al manipular las etiquetas de condicionamiento durante los pasos de *denoising*, "empujamos" matemáticamente un vector latente de una célula de control hacia el estado estimulado.
* **Decodificación y Evaluación:** Los vectores latentes perturbados se pasan a través del decodificador congelado del Autoencoder para recuperar los nuevos perfiles de 2000 genes. 
* **Clasificador "Juez":** Un clasificador Random Forest, actuando como juez biológico, se entrena con datos reales para evaluar cuantitativamente si las células perturbadas sintéticamente exhiben genuinamente las características de las células estimuladas reales.

## Tecnologías y Librerías
* **Deep Learning:** PyTorch (`torch`, `torch.nn`, `torch.optim`)
* **Bioinformática / scRNA-seq:** Scanpy (`sc`), AnnData
* **Machine Learning:** Scikit-Learn (Random Forest, Standard Scaler, Label Encoding)
* **Manipulación y Visualización de Datos:** Pandas, NumPy, Matplotlib, Seaborn (Proyecciones UMAP/PCA)
* **Bioinformatics/scRNA-seq:** Scanpy (`sc`), AnnData
* **Machine Learning:** Scikit-Learn (Random Forest, Standard Scaler, Label Encoding)
* **Data Manipulation & Visualization:** Pandas, NumPy, Matplotlib, Seaborn (UMAP/PCA projections)
