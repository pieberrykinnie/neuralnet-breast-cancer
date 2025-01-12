# Neural Network Breast Cancer Prediction

A project demonstrating the use of R's `neuralnet` package to predict breast cancer diagnoses using the Wisconsin Breast Cancer Dataset.

## Overview

This project implements a neural network to classify breast tumors as either benign or malignant based on cell nuclei features. Using the Wisconsin Breast Cancer Dataset, which contains measurements from 569 breast mass samples, the model achieves up to 96.83% accuracy in classification.

## Dataset

The Wisconsin Breast Cancer Dataset includes:
- 569 instances
- 32 attributes per instance
- Binary classification: Benign (B) or Malignant (M)
- Features include measurements like radius, texture, perimeter, area, smoothness, etc.

Reference to dataset details:

````41:57:neuralnet-breast-cancer.Rmd
1) ID number
2) Diagnosis (M = malignant, B = benign)
3-32)

Ten real-valued features are computed for each cell nucleus:

	a) radius (mean of distances from center to points on the perimeter)
	b) texture (standard deviation of gray-scale values)
	c) perimeter
	d) area
	e) smoothness (local variation in radius lengths)
	f) compactness (perimeter^2 / area - 1.0)
	g) concavity (severity of concave portions of the contour)
	h) concave points (number of concave portions of the contour)
	i) symmetry 
	j) fractal dimension ("coastline approximation" - 1)
```
````


## Implementation

The project uses R's `neuralnet` package to create and train neural networks. Key aspects include:

1. Data preprocessing
   - Removal of ID column
   - No missing values handling required
   - 2:1 split for training/validation data

2. Neural Network Architecture
   - Input layer: 30 neurons (features)
   - Hidden layers: Various configurations tested
   - Output layer: 2 neurons (Benign/Malignant)

3. Model Variations Tested:
   - Single hidden node
   - Two hidden nodes
   - Three hidden nodes
   - Two layers with two nodes each

The best performing model used:

````317:319:neuralnet-breast-cancer.Rmd
```{r}
fifth_net <- neuralnet((Diagnosis == "B") + (Diagnosis == "M")~., train_set,
                        hidden = c(2,2), rep = 5)
````


## Results

The project tested multiple neural network configurations:

1. Single hidden node: 69.31% accuracy (baseline)
2. Two hidden nodes: 95.77% accuracy
3. Three hidden nodes with modifications: 94.18% accuracy
4. Two layers (2,2): 96.83% accuracy (best performing)

## Dependencies

- R
- neuralnet package
- Standard R libraries for data manipulation

## Usage

1. Install required R packages:
```R
if (!require("neuralnet")) {
  install.packages("neuralnet")
  library("neuralnet")
}
```

2. Load and prepare the dataset:
```R
cancer <- read.csv("https://raw.githubusercontent.com/julien-arino/math-of-data-science/refs/heads/main/CODE/wdbc.csv", header = FALSE)
```

3. Follow the implementation steps in the R Markdown document for training and prediction.

## References

1. National Breast Cancer Foundation
2. American Cancer Society
3. Wisconsin Breast Cancer Dataset
4. neuralnet R package documentation

Full references available in:

```333:343:neuralnet-breast-cancer.Rmd
## References

1. https://www.nationalbreastcancer.org/breast-cancer-facts/
2. https://www.cancer.org/cancer/types/breast-cancer/about/how-common-is-breast-cancer.html
3. https://pmc.ncbi.nlm.nih.gov/articles/PMC10772314/
4. https://pages.cs.wisc.edu/~olvi/uwmp/cancer.html
5. https://raw.githubusercontent.com/julien-arino/math-of-data-science/refs/heads/main/CODE/wdbc.csv
6. https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic
7. https://github.com/bips-hb/neuralnet
8. https://atm.amegroups.org/article/view/10492/11983
9. https://stackoverflow.com/questions/43795530/knitr-and-plotting-neural-networks
```

## Author

Peter Vu

## License

This project is available for educational and research purposes. Please refer to the original dataset and package licenses for usage restrictions.