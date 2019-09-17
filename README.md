# Wisconsin-Diagnostic-Breast-Cancer

The objective of this project was to choose a dataset, verify the source of the data, and perform end-to-end data analysis process. The data analysis process included steps - reading and cleaning the data; exploratory data analysis to understand the distribution of the data, evaluate outliers, and examine correlations between features and target variables; and building and verifying the model using regression analysis.

## Dataset Description

Using the Breast Cancer Wisconsin (Diagnostic) dataset for the final project. The source of the data is UCI Machine Learning Repository, a reliable and reputable data source in the machine learning community. 

#### Dataset Information
The dataset is created by Dr. William H Wohlberg, O. L. Mangasarian, and W.N Street at the University of Wisconsin. All the information about the dataset is publicliy available and has been used by other organizations such as universities in the US, National University of Singapore, Microsoft Reserach and more.

Features are computed from a digitized image of a fine needle aspirate (FNA) of a breast mass and describe characteristics of the cell nuclei present in the image.

Separating plane described above was obtained using Multisurface Method-Tree (MSM-T), a classification method which uses linear programming to construct a decision tree. Relevant features were selected using an exhaustive search in the space of 1-4 features and 1-3 separating planes. 


## Conclusions

- I started with validating the source of the dataset, counting the columns and rows, and looking for null or missing values. The dataset is well organized and clean. I examined the columns and realized that some columns were dependent on all the mean columns so decided to remove them from the dataset.

- Class imbalance in our dataaset with 63% benign cases(357) and 37% malignant(212). We saw this distribution in our model too with the testing dataset. 

- Density plots and histograms of the attributes show that the data is rightly skewed and follows a log normal distribution and even after normalization and scaling the data is still skewed.

- Since my sample size is <1000 I used Shapiro-Wilk test to check my null hypothesis which is that the data is normally distributed. Since in all the cases my p-values are less than 0.05, I will reject null hypothesis. Event the Anderson-Darling test rejects the null hypothesi.

- Next I used the D’Agostino’s K^2 test to check the skewness of the data. Since K^2 > 1 for the features, data is positively and highly skewed with a long right tail. This is evident in the density and histogram plots. 

- It is established that the data is not normally distributed and linear regression is not applicable. Logistic regression predicts probability between 0 and 1 of a categorical response variable. I used binary logitic regression as my categorical variable has two outcomes 'Benign' or 'Malignant'

- I used boxplots for visualizing the outliers and noticed that the dataset does not contain too many outiers. I chose 'area_mean' to calculate the Zscore to determine the number of outliers for that column. Since the number is not very high, I prefered removing those outliers from the dataset and took all the datapoints >2.5 to use it for the model.

- The residual plot shows that the points are not randomly dispersed, so we have to use a non-linear model

- I removed features that showed strong multicolinearity. My goal was to ensure that the model is a great fit by removing independent variables that show high correlation. The reason for this is that if there is a high correlation between two features then that would make it impossible to accurately test how a feature A is affecting Y (target) independent of feature B. Using the correlation matrix I find that perimeter and radius are highly dependent on each other, and concavity has a strong relationship with concave_points_mean, and compactness so I removed them. 

- **Radius, perimeter, and area** have strong correlations which is expected as perimeter = 2*pi*radius and area = pi*radius^2. So, we can remove perimeter and area from our dataset.

- Similary, **concavity, concave points, and compactness** show multicolinearity, since concavity has the strongest correlation with the other two, I will remove it. 

- **H(0): No relationship between diagnosis and feature ; H(1): There exists a relationship between diagnosis and feature; P-value threshold = 0.05**

- I built my model using the other featuers and evaluated the p-values of the features using summary(). I find that area, smoothness, and symmetry have p-values > 0.05. In these cases, I rejected the null hypothesis. 

- The area under the curve (AUC) is 0.83 of the ROC plot, so the model is highly capable of distinguishing and labeling the diagnosis. AUC is the measurement of separaability and higher the value better the model is at distingusing between patients with disease or no disease.

