# Thesis: Simulation and Analytical Framework for T2D Risk Factor Progression and Disease Onset
### Data Simulation Using UKPDS 90 Model
- Simulated longitudinal patient-level data for HbA1c (systolic blood pressure (SBP), and total cholesterol maybe later) based on the dynamic model presented in UKPDS 90: Estimating risk factor progression equations for the UKPDS Outcomes Model 2.
- The simulation is governed by the following autoregressive mixed model:
	yi,t = ϕ0 + ϕ1 yi,t−1 + γ ln(yearit) + ϕ2 yi,0 + ϕ3 sexi + βj ethnicij + μi + ϵit 
where 𝑦𝑖,𝑡 represents the value of the risk factor of interest for individual i in year t, 𝑦𝑖,𝑡−1 represents the one-year lag of the risk factor of interest and excludes value at randomization (or the three-year lag for the risk factors measured every 3 years), ln(𝑦𝑒𝑎𝑟𝑖𝑡) represents the log of diabetes duration in year t, yi,0 represents the initial risk factor measurement for individual i (excludes value at randomization), 𝑠𝑒𝑥𝑖 represents the sex of individual i (1=female, 0=male), 𝑒𝑡ℎ𝑛𝑖𝑐𝑖𝑗 represents the ethnicity j of individual i (where j=1 was Asian-Indian ethnicity, j=2 was Afro-Caribbean ethnicity, and the reference group white and other). The unobserved time-invariant heterogeneity is represented by 𝜇𝑖, and 𝜖𝑖𝑡 concerns the idiosyncratic error component. If more than one measurement of the risk factor was available in a given year, we used the average in the analysis. Finally, in our data t=1 corresponds to the first 12 months post-randomization and that diabetes duration, 𝑦𝑒𝑎𝑟𝑖𝑡, equals “0” in this period (i.e. newly diagnosed).
- Model parameters capture time dynamics, patient-specific heterogeneity, and demographic covariates (sex, ethnicity).
- Simulation parameters (e.g., duration of follow-up, dropout rates, average HbA1c range) were aligned with empirical values reported in the source publication.
### Assessment of Covariate Impact: Sex and Ethnicity
- Investigated the contribution of sex and ethnicity to inter-patient variability in simulated risk factor trajectories.
- Extracted and synthesized coefficient estimates from three peer-reviewed studies focusing on diverse type 2 diabetic populations
- Adjusted the simulation coefficients accordingly and re-evaluated the model output to quantify the marginal impact of varying demographic weights.
### Disease Progression Rate Estimation Based on HbA1c Dynamics
- Modeled the progression rate from baseline health status to microvascular complications as a function of HbA1c evolution using a multiplicative risk ratio framework: 
	Rate Level 2 = Rate Level 1 × (RF Level 2 / RF Level 1) ** β
- Derived from the study Effect of patients’ risks and preferences on health gains with plasma glucose level lowering in T2DM.
  - β reflects the elasticity of the hazard rate with respect to relative changes in the risk factor (e.g., HbA1c); different β values can encode varying intervention efficiencies or treatment responsiveness.
### Assignment of Initial Event Rates via Regression Model for Beta Analysis
- Since direct hazard rates for each HbA1c level were unavailable, interpolated them using estimates from Cost-effectiveness of intensive glycemic control, intensified hypertension control, and serum cholesterol level reduction for T2DM.
- Fitted a simplified linear regression model to establish a functional relationship between HbA1c levels and corresponding baseline hazard rates.
- These estimates formed the foundation for computing β values and rate progression over time in the presence of evolving HbA1c.
# Prediction of Microvascular Disease Probabilities
- Applied a fixed β value derived from literature to estimate disease rates over a defined time horizon.
-Computed cumulative probabilities of disease onset using the exponential decay model for event probabilities:
			P=1−e ** (-rate*time)
- This step links continuous risk factor progression to discrete disease outcomes under various modeling assumptions.
### Future Work
- First, in the current analysis, the beta analysis (indicating intervention efficiency) was applied to the general average results across the entire simulated cohort. However, in the original source article, separate coefficients are provided for specific patient groups treated with diet alone or with insulin therapy. As a next step, I aim to simulate data specifically for these therapy groups and apply the beta analysis separately to each subgroup. This will allow a more differentiated evaluation of disease progression under different treatment strategies and provide a more realistic and nuanced understanding of intervention effects across distinct patient populations.
- Second, to improve the realism and validity of the hazard rate estimation process, future work will focus on replacing the currently implemented linear regression model with a more biologically and empirically grounded approach. Specifically, hazard rates for microvascular complications (e.g., retinopathy) will be derived using the modeling framework and empirical findings from the landmark study:
"The Relationship of Glycemic Exposure (HbA1c) to the Risk of Development and Progression of Retinopathy in the Diabetes Control and Complications Trial."
This study offers a well-validated, non-linear relationship between cumulative glycemic exposure (HbA1c levels) and the hazard of developing or progressing diabetic retinopathy, one of the key microvascular complications of type 2 diabetes. Incorporating their hazard function or survival analysis-based approach into the simulation framework will:
  - Provide a more accurate mapping between HbA1c trajectories and disease risk.
  - Replace the currently assumed linear association with a model reflecting clinically observed saturation and threshold effects.
  - Enable better calibration of simulated disease probabilities to real-world data, improving the external validity of the results.
Ultimately, this enhancement will strengthen the link between the simulated risk factor trajectories and downstream clinical outcomes, making the simulation framework more suitable for policy evaluation, personalized treatment modeling, or cost-effectiveness analysis in type 2 diabetes care.

