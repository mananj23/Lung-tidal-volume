# ML-task2
secy recruitment task - MANAN JINDAL 230625
# FINDING DATASET
- I searched for tidal volume data set on google.com.  
- After a lot of searches, i finally got a suitable data set from "https://physionet.org/content/respiratory-dataset/1.0.0/#files-panel".
- This data set had two parts that were of my interest namely "subject-info.csv" which contained information of 80 subjects with features:
  - Sex (M/F)
  - Height [cm]
  - Weight [kg]
  - Age [years]
  - Asthma (Y/N)
  - history of smoking (Y/N)
  - history of Vaping (Y/N)
  - Chest Depth [mm]
  - Chest Width [mm]
- And another one is "processed_data"("https://physionet.org/content/respiratory-dataset/1.0.0/Processed_Dataset/#files-panel") which contains 80 CSV files each containing 
  data on their tidal volume with factors like time, Pressure[cmH2O]	Flow [L/s], V_tidal [L], Chest[mm], Abd[mm], Inspiratory Indicies	Time (Aeration Data)[s].
- Interested factor is V_tidal.
# MAKING THE FINAL DATA SET TO APPLY THE ML MODEL
- Now to make the final data set complete I had to create a column named "tidal volume" in "subject-info.csv".
- This column should contain the lung tidal volume that would act as our output.
- So first we need to analyze our processed_data file that contains 80 CSV files corresponding to 80 subjects.
- each of these CSV file contained a column " V_tidal [L] " which had around 1 lakh readings that varied with time.
- According to this article("https://www.ncbi.nlm.nih.gov/books/NBK482502/#:~:text=Tidal%20volume%20is%20the%20amount,proper%20ventilation%20to%20take%20place.") lung tidal volume is defined as the amount of air that moves in or out of the lungs with each respiratory cycle.
- So to get a better understanding i plotted a graph of tidal volume vs time of any one of the observations. The corresponding Python file is attached("analyisng_data_set").
 ![image not available](https://github.com/mananj23/ML-task/blob/main/analyzing_data_set.png?raw=true)
- here we can see that the distance between consecutive minima is the tidal lung volume ie the amount of air in and out during one respiratory cycle.
- So the best value would be the mean value of these jumps, which i calculated in my "ML_task_pclub.ipynb" file using simple numpy properties.
- Then i just attached a new column called averages in my "subject-info.xlsx" file to complete it and thus my final data set("final_data_set.xslx") is ready.
# Applying ML models
- Before applying ML models we need to do feature encoding ie making features such as Sex, history of vaping(Y/N), history of smoking(Y/N), etc to numerical values to apply ML models.
  ##  Linear Regression
    - After applying the linear regression model i got a mean absolute error of 0.2675275531904294.
    - This error is quite significant.
  ## Random Forest Regressor
    - For this model i uesd n_estimators_values = [50, 100, 150, 200, 250,350,450,550,650,750,850,950,1000].
    - For these estimators, i got the following mae:<br>
      n_estimators = 50, Mean Absolute Error: 0.21233410828171217
      n_estimators = 100, Mean Absolute Error: 0.20414702504280893<br>
      n_estimators = 150, Mean Absolute Error: 0.2073048123279492<br>
      n_estimators = 200, Mean Absolute Error: 0.20476390966409957<br>
      n_estimators = 250, Mean Absolute Error: 0.20093678466861872<br>
      n_estimators = 350, Mean Absolute Error: 0.20038107251243692<br>
      n_estimators = 450, Mean Absolute Error: 0.19903799606762307<br>
      n_estimators = 550, Mean Absolute Error: 0.20164575124640163<br>
      n_estimators = 650, Mean Absolute Error: 0.20457524386356885<br>
      n_estimators = 750, Mean Absolute Error: 0.20535197750416914<br>
      n_estimators = 850, Mean Absolute Error: 0.20639606421081502<br>
      n_estimators = 950, Mean Absolute Error: 0.2048977076787292<br>
      n_estimators = 1000, Mean Absolute Error: 0.2050708515568506<br>
     - These values of error are also quite high.
- These large errors are occurring due to less amount of training data.
- To decrease these errors i did augmentation of data by adding random noise to my data.
- I augmented data with a factor of 100 thus making a new data set with 8000 values.
 ## Random Forest Regressor post augmentation 
   - For this model i used n_estimators_values = [50, 100, 150, 200, 250,350,450,550,650,750,850,950,1000].<br>
     n_estimators = 50, Mean Absolute Error: 0.10028600920925321<br>
     n_estimators = 100, Mean Absolute Error: 0.10278071610033494<br>
     n_estimators = 150, Mean Absolute Error: 0.10272820873081782<br>
     n_estimators = 200, Mean Absolute Error: 0.10225012180627198<br>
     n_estimators = 250, Mean Absolute Error: 0.10114634338218383<br>
     n_estimators = 350, Mean Absolute Error: 0.10204418436271814<br>
     n_estimators = 450, Mean Absolute Error: 0.10252048722483989<br>
     n_estimators = 550, Mean Absolute Error: 0.10276701964897325<br>
     n_estimators = 650, Mean Absolute Error: 0.10236923517865253<br>
     n_estimators = 750, Mean Absolute Error: 0.10341185712907577<br>
     n_estimators = 850, Mean Absolute Error: 0.10337309560025168<br>
     n_estimators = 950, Mean Absolute Error: 0.10325500993070738<br>
     n_estimators = 1000, Mean Absolute Error: 0.1037772569759186<br>
![Alt text]()
   - After augmentation, the error decreased by a significant amount.
   - I have tried more models but forest regressor shows prominent results.
 ## XGBoost regressor model
   - Mean Squared Error: 0.133875599435572
 ## SVR(kernel='rbf')
   - Mean Squared Error: 0.2670534077733942
