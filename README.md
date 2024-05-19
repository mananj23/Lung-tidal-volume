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
# MAKING THE FINAL DATA SET TO APPLY THE ML MODEL
- Now to make the final data set complete I had to create a column namely "tidal volume" in "subject-info.csv".
- This column should contain the lung tidal volume that would act as our output.
- So first we need to analyze our processed_data file that contains 80 CSV files corresponding to 80 subjects.
- each of this CSV file contained a column " V_tidal [L] " which had around 1 lakh readings that varied with time.
- According to this article("https://www.ncbi.nlm.nih.gov/books/NBK482502/#:~:text=Tidal%20volume%20is%20the%20amount,proper%20ventilation%20to%20take%20place.") lung tidal volume is defined as the amount of air that moves in or out of the lungs with each respiratory cycle.
- So to get a better understanding i plotted a graph of tidal volume vs time of any one of the observations. The corresponding Python file is attached("analyisng_data_set").
- 
- 
