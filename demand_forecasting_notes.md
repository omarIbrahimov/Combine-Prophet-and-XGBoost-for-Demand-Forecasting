# Combine Prophet and XGBoost for Demand Forecasting

### 1.  Rossmann Store Sales: Initial Data Merging and Diagnostics
We prepare the data to work with it. First, we combine the train and store files, merge them to make our work on 1 file instead of 2. I decided to not use Customers as feature, therefore, removed them. In the end, some statistics are printed to show the general situation of the file.

#### 2. Exploratory Data Analysis: Sales Trends and Store Characteristics
The make the initial analysis, I chose 5 criterias:
1. Total Daily Sales over Time: This is more for to see the general situation. It shows how much the stores sold over the total time. 
2. Mean Sales by DayOfWeek: When we understand the situation for each day, we can make our predictions and deductions using that. For example, the situation on Sundays and Tuesdays differs completely as most of the stores are closed on weekends.
3. Mean Sales for Promo 0 and 1: We can see the difference the promotions are making and if they are helpful or not.
4. Mean Sales by StoreType and Assortment: This was made to see how each store type performs independently from others 
5. Number of Open Stores by Day: This is related to the 2nd point. It shows how many stores work on weekends.

### 3. Data Preparation: Filtering and Train/Validation Splits
Some data is skewed because there are holidays, weekends, some other special occasions. To fix this, I use the Mean Sales per Open Store.

### 4. Time Series Forecasting: Prophet Baseline Model
We use Prophet to see the trends for weekly and yearly basis. Then check for MAE,MAPE,RMSPE.

MAE:   2240.27
MAPE:  0.3888 (38.88%)
RMSPE: 0.5715 (57.15%)

### 5. Hybrid Residual Modeling with XGBoost
Because Prophet sees the general trends, we use XGBRegressor to see the store-specific dynamics to improve the algorithm

MAE:   1360.66
MAPE:  0.2257 (22.57%)
RMSPE: 0.3254 (32.54%)

### 6. Direct XGBoost Model (No Prophet Involvement)
MAE:   1384.73
MAPE:  0.2209 (22.09%)
RMSPE: 0.3152 (31.52%)



### 7. Final Model Evaluation & Comparison
We evaluated the Prophet, XGBoost and the Hybrid Model. Took all there MAE,MAPE,RMSPE results and compared them.


## Conclusion

The difference between the Hybrid model and Prophet alone is massive.
However, when compared to XGBoost only, the Hybrid model doesn't show big difference.

Therefore, I would rather use simple XGBoost instead of trying to combine the Prophet and XGBoost.
