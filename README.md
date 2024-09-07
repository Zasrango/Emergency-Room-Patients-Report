# Patient Health Care Project

# Emergency-Room-Patients-Report




Project Summary:

This project focuses on analyzing a healthcare dataset containing details about patient appointments. The key goal is to assess patient wait times, identify patterns in department referrals, and examine any potential correlations between patient demographics and healthcare service utilization. The dataset captures patient information such as age, race, gender, and department referral, which will be used to create metrics to enhance healthcare service efficiency and patient experience.

Key Insights from the Data:

Wait Time Analysis: Understanding which departments have higher patient wait times and analyzing possible reasons (e.g., peak hours, age, etc.).

Demographic Insights: Analyzing patient demographics such as gender, race, and age to identify trends in department referrals and service utilization.

Satisfaction Data (SAT Score): Although most SAT scores are missing, once captured, these can be used to evaluate patient satisfaction in relation to wait times and other factors.

For all new to DAX can help themselves out with these formulas :

Key Performance Indicators (KPIs) for the Report:

Total patients - Total_Patients = DISTINCTCOUNT(Patients_Dataset[patient_id])

Total Patients By Department referrals - % Reffered Patients = VAR _Filterpatients= CALCULATE([Total_Patients],Patients_Dataset[department_referral]<>"none")
                     RETURN
                     DIVIDE(_Filterpatients,[Total_Patients])

Unreffered Patients - % UnReffered Patients = VAR _Filterpatients= CALCULATE([Total_Patients],Patients_Dataset[department_referral]= "None")
                     RETURN
                     DIVIDE(_Filterpatients,[Total_Patients])
                     
  Administrative % = DIVIDE(COUNTROWS(FILTER(Patients_Dataset,Patients_Dataset[patient_admin_flag]=TRUE())),[Total_Patients])

  Non Administrative % = DIVIDE(COUNTROWS(FILTER(Patients_Dataset,Patients_Dataset[patient_admin_flag]=FALSE())),[Total_Patients])

 Avrage Satisfaction Score = CALCULATE(AVERAGE(Patients_Dataset[patient_sat_score]),Patients_Dataset[patient_sat_score]<>BLANK())                     

 Average wait time = AVERAGE(Patients_Dataset[patient_waittime])

 % No rating = VAR _noratings= CALCULATE([Total_Patients],
                Patients_Dataset[patient_sat_score]=BLANK())
                return
                DIVIDE(_noratings,[Total_Patients])

% Male Visits = DIVIDE(CALCULATE([Total_Patients],Patients_Dataset[patient_gender]="M"),[Total_Patients])

% Females Visits = DIVIDE(CALCULATE([Total_Patients],Patients_Dataset[patient_gender]="F"),[Total_Patients])

% Unknown Visits = DIVIDE(CALCULATE([Total_Patients],Patients_Dataset[patient_gender]="NC"),[Total_Patients])                

--My HeatMap measure ---

Age Buckets = SWITCH(TRUE(),
                            Patients_Dataset[patient_age]<=10,"0-10",
                             Patients_Dataset[patient_age]<=20,"11-20",
                              Patients_Dataset[patient_age]<=30,"21-30",
                               Patients_Dataset[patient_age]<=40,"31-40",
                                Patients_Dataset[patient_age]<=50,"41-50",
                                 Patients_Dataset[patient_age]<=60,"51-60",
                                  Patients_Dataset[patient_age]<=70,"61-70",
                                  "70+")

Measure to distingush between different age groups --

Age Group = Var _Patientsage = Patients_Dataset[patient_age]
             return
             IF(_Patientsage<=2, "Infant",
             IF(_Patientsage<=6, "Early Childhood",
             IF(_Patientsage<=12 , "Middle Childhood",
             IF(_Patientsage<=18,"Teenager",
             "Adult"))))

![Screenshot 2024-09-07 213157](https://github.com/user-attachments/assets/9fb648e5-0f0d-442e-b907-a3035d231f3f)

                            

 

  

