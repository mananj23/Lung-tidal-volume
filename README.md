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
 ![Alt text]( https://miro.medium.com/v2/resize:fit:1100/format:webp/0*4hfu8vepPsbjTBuH.png)
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
## Augmentation of data
- These large errors are occurring due to less amount of training data.
- To decrease these errors i did augmentation of data by adding random noise to my data.
- I augmented data with a factor of 100 thus making a new data set with 8000 values.
 ## Random Forest Regressor post augmentation 
   - For this model i again used n_estimators_values = [50, 100, 150, 200, 250,350,450,550,650,750,850,950,1000].<br>
     n_estimators = 50, Mean Absolute Error: 0.08305533410717278<br>
     n_estimators = 100, Mean Absolute Error: 0.08266682918370115<br>
     n_estimators = 150, Mean Absolute Error: 0.0824750813811108<br>
     n_estimators = 200, Mean Absolute Error: 0.08236409762442887<br>
     n_estimators = 250, Mean Absolute Error: 0.08233542614027277<br>
     n_estimators = 350, Mean Absolute Error: 0.08228541755895728<br>
     n_estimators = 450, Mean Absolute Error: 0.08223107675110898<br>
     n_estimators = 550, Mean Absolute Error: 0.08223550402875503<br>
     n_estimators = 650, Mean Absolute Error: 0.08221470993210422<br>
     n_estimators = 750, Mean Absolute Error: 0.0821863426046198<br>
     n_estimators = 850, Mean Absolute Error: 0.08217939117429128<br>
     n_estimators = 950, Mean Absolute Error: 0.08216155016348622<br>
     n_estimators = 1000, Mean Absolute Error: 0.08215998756137491<br>
![Alt text](https://github.com/mananj23/ML-task/blob/main/clips.png?raw=true)
 ### Here are weights for n_estimators_values = [50, 100]
     - n_estimators = 50:
       - Tree 50 feature importances:
       - Age [years]: 0.0315481020740988
       - Weight [kg]: 0.15994010959420563
       - Height [cm]: 0.0826936777637561
       - Chest Depth [mm]: 0.008355292096388738
       - Chest Width [mm]: 0.7083550884876183
       - Sex (M/F): 0.00900811848870871
       - Asthma (Y/N): 3.5374816754303314e-06
       - History of Smoking (Y/N): 9.607401354841729e-05
       - History of Vaping (Y/N): 0.0
     - n_estimators = 100:
       - Tree 100 feature importances:
       - Age [years]: 0.04588730862556338
       - Weight [kg]: 0.16008439538992386
       - Height [cm]: 0.15470505100913523
       - Chest Depth [mm]: 0.0565026353684797
       - Chest Width [mm]: 0.581300224733573
       - Sex (M/F): 9.063502129580747e-07
       - Asthma (Y/N): 0.00028169588388134024
       - History of Smoking (Y/N): 0.00014881733822808352
       - History of Vaping (Y/N): 0.001088965301002507
   - After augmentation, the error decreased by a significant amount.
   - I have tried more models but forest regressor shows prominent results.
 ## XGBoost regressor model
   - Mean Squared Error: 0.133875599435572
 ## SVR(kernel='rbf')
   - Mean Squared Error: 0.24995713806142078
