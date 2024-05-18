# ML-task
secy recruitment task 
# FINDING DATASET
- I searched for tidal volume data set on google.com.  
- After a lot of searches, i finally got a suitable data set from "https://physionet.org/content/respiratory-dataset/1.0.0/#files-panel".
- This data set had two parts which were of my interest namely "subject-info.csv" which contained information of 80 subjects with features:
 - Sex (M/F)
 - Height [cm]
 - Weight [kg]
 - Age [years]
 - Asthma (Y/N)
 - history of smoking (Y/N)
 - history of Vaping (Y/N)
 - Chest Depth [mm]
 - Chest Width [mm]
- And another one is "processed_data"("https://physionet.org/content/respiratory-dataset/1.0.0/Processed_Dataset/#files-panel") which contains 80 CSV files each containing data on their tidal volume with factors like time, Pressure[cmH2O]	Flow [L/s], V_tidal [L], Chest[mm], Abd[mm], Inspiratory Indicies	Time (Aeration Data)[s].
- Interested factor is V_tidal.
- I have attached link
# CLEANING AND MAKING THE FINAL DATA SET TO APPLY THE ML MODEL
- Now to make the final data set I had to create a column namely "tidal volume" in "subject-info.csv" that i manually filled with the tidal volume in the "proceesed_data" folder.The tidal colume i filled was the average, according to sources i studied about tidal volume online.
- Then i cleaned the data.
- The final data set that i used for prediction is attached in my git repository.
  
