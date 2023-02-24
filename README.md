## House-Price-Analysis--Machine-Learning

**Background**

Using the USA house price data to determine the factors that influence house price

**Dataset**

This data is a Kaggle dataset on U.S. house prices.

**Housing dataset**

	SalePrice	final sale price
	LotFrontage	width of lot on street
	LotArea		square feet of lot
	OverallQual	quality of house on scale of 1 to 10
	OverallCond	condition of house on scale of 1 to 10
	YearBuilt	calendar year of construction
	BsmtFin	square feet of finished basement
	TotalBsmtSF	total square feet of basement (finished and unfinished)
	1stFlrSF	square feet of first floor
	2ndFlrSF	square feet of second floor
	LivArea		square feet of living area
	BsmtFullBath	number of full bathrooms in basement
	BsmtHalfBath	number of half bathrooms in basement
	FullBath	number of full bathrooms above ground
	HalfBath	number of half bathrooms above ground
	Bedroom	number of bedrooms
	Kitchen		number of kitchens
	TotRmsAbvGrd	number of rooms above ground
	Fireplaces	number of fireplaces
	GarageCars	number of garage spaces for cars
	GarageArea	square feet of garage
	WoodDeckSF	square feet of wood deck
	PoolArea	square feet of pool area
  
  **DATA VISUALIZATION**
  
  ![image](https://user-images.githubusercontent.com/100436462/221032594-b48c21bf-b945-4bdb-9152-8609d59ea7e1.png)

![image](https://user-images.githubusercontent.com/100436462/221032728-41bc9035-36c5-4538-920b-da0a79d9b601.png)

**VIF ANALYSIS**

![image](https://user-images.githubusercontent.com/100436462/221032901-6501c99a-73aa-473c-b779-cf94548a7cbf.png)

![image](https://user-images.githubusercontent.com/100436462/221032974-ca6bcb8f-1ee9-48d0-9fa6-e7ce50156474.png)

**NEURAL NETWORK WITH ONE HIDDEN LAYER**

install.packages("neuralnet", dependencies = TRUE)

library(neuralnet)

housing_index <- sample(nrow(Housing), 1/2 * nrow(Housing))

housing_train <- Housing[housing_index, ]

housing_test <- Housing[-housing_index, ]

head(housing_train)

 head(housing_test)
 
normalize <- function(x) {return((x-min(x))/(max(x)-min(x)))}

trainingnorm <- as.data.frame(lapply(housing_train,normalize))

testingnorm <- as.data.frame(lapply(housing_test,normalize))

housingnet <- neuralnet(SalePrice ~PoolArea+BsmtHalfBath+ WoodDeckSF+ LotArea+ OverallCond+ Kitchen+ LotFrontage+ Fireplaces+ BsmtFullBath+ HalfBath+ Bedroom+ BsmtFin+ FullBath+ OverallQual+ YearBuilt+ TotalBsmtSF+ TotRmsAbvGrd+ GarageArea+ GarageCars, trainingnorm, lifesign="minimal", linear.output=TRUE, threshold=0.01)

plot(housingnet)

![image](https://user-images.githubusercontent.com/100436462/221033564-2eeb4ead-a069-4af3-b42d-1e72b538a1e0.png)

**TESTING DATA**

temp_test <- subset(testingnorm, select = c("PoolArea","BsmtHalfBath","WoodDeckSF",
"LotArea","OverallCond","Kitchen","LotFrontage","Fireplaces","BsmtFullBath",
"HalfBath","Bedroom","BsmtFin","FullBath", "OverallQual", "YearBuilt", "TotalBsmtSF", "TotRmsAbvGrd", "GarageArea", "GarageCars"))

head(temp_test)

housingnet_results <- compute(housingnet, temp_test)

predicted_price <- housingnet_results$net.result

cor(predicted_price, testingnorm$SalePrice)

![image](https://user-images.githubusercontent.com/100436462/221033984-8d404374-aa0e-4d30-a084-41a68f84a79b.png)

**NEURAL NETWORK WITH TWO HIDDEN LAYERS**

install.packages("neuralnet", dependencies = TRUE)

library(neuralnet)

housing_index <- sample(nrow(Housing), 1/2 * nrow(Housing))

housing_train <- Housing[housing_index, ]

housing_test <- Housing[-housing_index, ]

head(housing_train)

 head(housing_test)
 
normalize <- function(x) {return((x-min(x))/(max(x)-min(x)))}

trainingnorm <- as.data.frame(lapply(housing_train,normalize))

testingnorm <- as.data.frame(lapply(housing_test,normalize))

housingnet <- neuralnet(SalePrice ~PoolArea+BsmtHalfBath+WoodDeckSF+LotArea+OverallCond
+ Kitchen+LotFrontage+Fireplaces+BsmtFullBath+HalfBath+Bedroom+ BsmtFin+ FullBath
+OverallQual+YearBuilt+TotalBsmtSF+TotRmsAbvGrd+ GarageArea+ GarageCars, trainingnorm, hidden=c(2,2), lifesign="minimal", linear.output=TRUE, threshold=0.01)

plot(housingnet)

![image](https://user-images.githubusercontent.com/100436462/221034480-cfee0984-325c-4776-9c37-2ccee4ceb2ee.png)

![image](https://user-images.githubusercontent.com/100436462/221034537-f807cde5-5d9c-43ff-b5bc-201ed19169ff.png)

**COMPARISION BETWEEN DIFFERENT NEURAL NETWORKS**

![image](https://user-images.githubusercontent.com/100436462/221034868-4ff7a66c-5db5-4f33-9954-f452d6bb1237.png)

**CONCLUSION**

Adding more hidden layers and hidden nodes doesn't always increase the accuracy of the Neural Network .

The following factors are most important in helping to predict house prices :
1.BsmtFin
2.Living Area
3.Garage Area
4.Total Basement SF
5.1st Floor SF









	
