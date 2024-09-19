# Nearest Earth Objects (NEO) Analysis
Project submission for *Aygaz Makine Öğrenmesi Bootcamp*!<br>
The analysis also can be found on my [Kaggle](https://www.kaggle.com/code/barberkengl/nasa-neos-supervised-unsupervised) Notebook.

## Dataset
**Source**: [NASA Nearest Earth Objects (1910-2024)](https://www.kaggle.com/datasets/ivansher/nasa-nearest-earth-objects-1910-2024)

The dataset contains information about objects classified as Near-Earth Objects (NEOs), collected between 1910 and 2024. These objects are potentially hazardous and are tracked for their size, velocity, and miss distance from Earth.

### Key Columns:
- **neo_id**: Unique identifier for each NEO.
- **name**: Name of the NEO.
- **absolute_magnitude**: The absolute magnitude of the object.
- **estimated_diameter_min**: Minimum estimated diameter of the object.
- **estimated_diameter_max**: Maximum estimated diameter of the object.
- **orbiting_body**: The celestial body the NEO is orbiting around.
- **relative_velocity**: The relative velocity of the NEO (in km/h).
- **miss_distance**: The closest distance from Earth during a flyby (in km).
- **is_hazardous**: A boolean indicating whether the object is classified as hazardous.

---

## Models and Analysis

### Data Preprocessing
Before applying the models, the dataset was cleaned and preprocessed:
- Missing values were handled using **mean imputation** for columns like `absolute_magnitude`, `estimated_diameter_min`, and `estimated_diameter_max`.
- Categorical features were encoded using **Label Encoding**.
- Numerical features were **scaled** using the **MinMaxScaler**.

### Unsupervised Learning

1. **K-Means Clustering**:
   - The dataset was clustered using K-Means to identify natural groupings within the data.
   - Elbow method and silhouette scores were used to determine the optimal number of clusters (3 clusters were chosen).
   
   **Scores** (after PCA):
   - **Silhouette Score**: 0.423
   - **Calinski-Harabasz Score**: 15,618
   - **Davies-Bouldin Score**: 0.664

2. **DBSCAN Clustering**:
   - DBSCAN was used to identify clusters based on the density of points.
   - Number of clusters: 3

   **Scores** (after PCA):
   - **Silhouette Score**: 0.775
   - **Calinski-Harabasz Score**: 2,148
   - **Davies-Bouldin Score**: 1.18

3. **Gaussian Mixture Model (GMM)**:
   - GMM was applied to the data as a probabilistic clustering method, also with 3 components.
   
   **Scores**:
   - **Silhouette Score**: 0.362
   - **Calinski-Harabasz Score**: 12,343
   - **Davies-Bouldin Score**: 0.922

  ![Unsupervised Table](https://cdn.discordapp.com/attachments/934138376452464650/1286416789340684359/image.png?ex=66edd47f&is=66ec82ff&hm=12160ff2b9e8d241254c77b7c28c45676154d1042f97288cfaa4051a0e4a0386&)

---

### Supervised Learning

1. **Logistic Regression**:
   - Used to classify NEOs as hazardous or non-hazardous.
   - Achieved an **accuracy of 87.17%** on the test set after **RandomizedSearchCV** for hyperparameter tuning.

2. **Random Forest Classifier**:
   - A Random Forest model was trained to improve the classification of hazardous NEOs.
   - With SMOTE applied to balance the dataset, the model achieved an **accuracy of 94.00%** on the test set, and **96.88%** on the training set after hyperparameter tuning.

  ![Supervised Table](https://cdn.discordapp.com/attachments/934138376452464650/1286416936170688594/image.png?ex=66edd4a2&is=66ec8322&hm=d22de5ce9da4d94237ca480a30b2f8f72c3c3cc375503bb5f7d3b4bc0ad89bdf&)

---

## Final Results

After evaluating both unsupervised and supervised methods, it was found that the **supervised learning models (Logistic Regression and Random Forest)** provided more accurate and interpretable results for predicting whether an NEO is hazardous. The **Random Forest Classifier** performed particularly well with a test accuracy of **94.00%** and an AUC score of **0.99**.

Given the dataset’s labeled nature and the task’s objective (predicting whether an NEO is hazardous), **supervised learning** proved to be the most appropriate approach.
