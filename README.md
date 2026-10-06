# Explainable Machine Learning for Progression-Free Survival in Prostate Cancer

Research code accompanying the doctoral study published in JMIR Cancer
Explainable Machine Learning–Based Prediction of Progression-Free Survival in Prostate Cancer: Retrospective Cohort Study

📄 Full article: JMIR Cancer
🧠 Why this project?
This project is part of my doctoral research in Digital Public Health and AI in Healthcare.
More than simply developing a high-performing model, this study changed my philosophy of how AI should be developed for healthcare.
A high-performing model is not necessarily a good model.

When evaluating an AI model, it is tempting to focus on:
AUC
Accuracy
C-index
F1-score
Other performance metrics

But performance is only meaningful when the underlying data and evaluation process are sound. If the data are incorrectly managed, labels are inappropriate, longitudinal information is ignored, missing data are handled incorrectly, or there is data leakage, a model can produce exceptionally high performance while having little or no real clinical value. If the data are wrong, even 100% accuracy does not make the model valid. For this reason, a model with impressive performance should not automatically be accepted as a baseline model unless the data preparation, feature construction, longitudinal structure, and evaluation methodology are also appropriate.

This became one of the most important methodological issues I had to clarify during the peer-review process of this study.

🏥 Clinical AI: The Data Come First
Clinical data are not simply a static table.
Patients usually interact with healthcare systems repeatedly:
Visit 1 → Visit 2 → Laboratory tests → Treatment → Follow-up → Progression
Therefore, clinical datasets often contain an important longitudinal structure.
In this study, the dataset contained:
212 patients, 478 longitudinal observations
Data collected over approximately 6 years
Clinical variables
Laboratory measurements
Treatment information
Rather than treating all variables as a single one-time observation, we first considered the distinction between:

Static features
Characteristics that generally remain stable or change slowly.Examples include: Demographic characteristics, Baseline characteristics

Dynamic features -Variables that can change throughout the patient's clinical trajectory. Examples include: Laboratory measurements, Treatment-related variables, Follow-up measurements

The dynamic features were used to represent the longitudinal nature of the patient data.
A recurrent autoencoder was then used to learn lower-dimensional latent representations of these longitudinal patterns.

The study compared four major approaches:
Cox Proportional Hazards (CPH)
Random Survival Forest (RSF)
Gradient Boosting Survival (GBS)
Deep Neural Network Survival Model

The final framework integrated:
Recurrent Autoencoder + Random Survival Forest + SHAP

📊 Key Results
RSF demonstrated improved discriminative performance and balanced calibration, achieving a C-index of 0.906 and AUCs of 0.941 and 0.917 at 4 and 5 years (IBS=0.0698). In contrast, the traditional CPH model performed poorly (C-index 0.531 and AUC 0.706 at 4 years and 0.833 at 5 years). Deep survival (AUCs of 0.941 at 4 years and 0.917 at 5 years, C-index 0.719, and IBS=0.0887) and GBS (AUCs of 0.765 at 4 years and 0.833 at 5 years, C-index 0.844, and IBS=0.0590) models showed moderate performance. SHAP analysis identified sodium, alanine aminotransferase, mean corpuscular hemoglobin, platelet count, and specific treatment categories as key drivers of increased progression risk.

💡 What I Learned from This Study

🔹 For clinicians reviewing AI results
When someone shares an AI result, don’t look only at the AUC, accuracy or performance metrics. A model can produce impressive numbers, but that does not automatically make it clinically useful. Before trusting an AI result, check whether the study has thought about the sequential longitudinal nature of the data, how they handle the missing information, whether it has an explainability component, and whether it makes clinical sense.
This becomes even more important when working with Transformers or agentic LLMs, where computational, financial, and environmental costs can be substantial and where handling messy clinical data is often far more difficult than the model architecture itself.
🔹 For AI developers, computer scientists & engineers
Clinical data is not just a table. In this study, rather than feeding every HMIS variable directly as a one-time point, patients normally come to the clinic, so we need to treat them as longitudinal data. In my study, I used an autoencoder to handle that problem, but I didn't put all variables in; I first separated static and dynamic features and focused on the dynamic features to better represent the longitudinal nature of patient data while keeping the modelling approach computationally practical.
One of the most important lessons from this study is that model performance is only meaningful when the underlying data and evaluation process are sound. Even if a model achieves exceptionally high performance, it should not automatically be accepted as a baseline if the data have been incorrectly managed or the evaluation is flawed. If the data are wrong, even 100% accuracy does not make the model valid or clinically meaningful. This was also one of the key methodological points I had to repeatedly clarify during the review process with the reviewers.


⚠️ Important Clinical Disclaimer
This model is a research prototype. It has not been externally validated in independent populations and should not be used to make clinical decisions or determine individual patient treatment. The study was based on a retrospective cohort from a single national cancer centre. Before clinical implementation, further validation is required using:
Larger cohorts, Multiple institutions, Independent populations
External validation datasets
Potentially multi-omics data
Prospective clinical evaluation

📚 Publication

Hein Minn Tun et al.
Explainable Machine Learning–Based Prediction of Progression-Free Survival in Prostate Cancer: Retrospective Cohort Study.
JMIR Cancer. 2026.
📄 Read the full article
👨‍💻 Author

Dr Hein Minn Tun
PhD Candidate in Digital Public Health – Specialised in AI in Healthcare
PAPRSB Institute of Health Sciences | School of Digital Science
Universiti Brunei Darussalam

🔗 Citation
If you use this repository or build upon this work, please cite the associated publication.

⭐ Final Thought
Clinical AI should not be judged by performance alone.
Trustworthy data → appropriate modelling → rigorous evaluation → explainability → clinical meaning.
That is the philosophy behind this project.
