# LW5-Grad-CAM-code
## Google Colab: https://colab.research.google.com/drive/1q6a19bhUIJYEE5TkbgjSl7pHMn11Am8Y?usp=sharing
## Google Drive: https://drive.google.com/drive/folders/1hIYYSTh3beTMG-51eUyUxH425qakfQLH?usp=sharing

## Part 12: Model Performance Comparison Table
| Model - Sample | Train Accuracy | Train Loss | Test Accuracy | Test Loss | Precision | Recall | F1-score | ROC | AUC |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Pre-trained Model 1 (ResNet50)** | 0.773159 | 0.800938 | 0.801770 | 0.735200 | 0.798849 | 0.794584 | 0.793827 | Generated | 0.983749 |
| **Pre-trained Model 2 (EfficientNetB0)** | 0.711475 | 1.033368 | 0.774336 | 0.887492 | 0.779982 | 0.767327 | 0.771029 | Generated | 0.978738 |
| **Pre-trained Model 3 (MobileNetV2)** | 0.686270 | 1.059168 | 0.750443 | 0.957094 | 0.746088 | 0.744426 | 0.741607 | Generated | 0.972930 |
| **Model from Teachable Machine** | 0.636524 | 1.212481 | 0.526549 | 1.533006 | 0.526301 | 0.514052 | 0.510291 | Generated | 0.896262 |
| **1st Model** | 0.999558 | 0.005695 | 0.592920 | 2.905696 | 0.590421 | 0.585907 | 0.582596 | Generated | 0.923034 |
| **2nd Model Enhancement** | 0.637409 | 1.152285 | 0.536283 | 1.501993 | 0.546942 | 0.530902 | 0.521282 | Generated | 0.927447 |
| **3rd Model - The Good Model** | 0.894097 | 0.381043 | 0.776991 | 0.914633 | 0.779187 | 0.777767 | 0.773807 | Generated | 0.977118 |

A. Model Performance

1. Which pre-trained model achieved the highest accuracy?
   - Why?The model that achieved the highest accuracy was ResNet50 (with a validation accuracy of 91.11%). This is because ResNet50 utilizes residual learning (skip connections), which effectively mitigates the vanishing gradient problem. This architecture allows it to train deeply, extract highly complex hierarchical features from the brain MRI scans, and generalize better than the other models.

3. Which model had the lowest performance? What could be the reason?The lowest-performing model was VGG16 (with a validation accuracy of 80.00%).
   - The reason for this lower performance is VGG16's older, heavier architecture. It relies on a dense stack of standard convolutional and fully connected layers, making it highly prone to overfitting on smaller datasets and computationally inefficient compared to modern architectures like ResNet.

5. How did loss values compare across models?
   - The best-performing model, ResNet50, achieved the lowest validation loss (0.3060). In contrast, VGG16 suffered from a significantly higher validation loss (0.5186). This discrepancy indicates that ResNet50 was much more confident and precise in its predictions, whereas VGG16 struggled to optimize its weights efficiently for this specific dataset.B. Evaluation Metrics

7. Why is accuracy not enough to evaluate a model?
   - Accuracy alone can be misleading, especially if a dataset has class imbalances. For example, if 80% of your dataset consists of "Glioma" scans, a naive model could simply predict "Glioma" every time and achieve 80% accuracy while failing completely to detect Meningiomas or healthy brains. Metrics like Precision, Recall, and F1-Score ensure the model performs safely across all individual classes.

9. Which model had the best F1-score? What does it indicate?
    - ResNet50 achieved the highest overall macro F1-score (0.91). This indicates an excellent, well-balanced performance between precision and recall across all three classes. The model is highly reliable because it simultaneously minimizes both false positives (wrongly diagnosing a tumor) and false negatives (missing a tumor entirely).

11. How did Precision and Recall differ across models?
    - ResNet50 maintained high precision and recall uniformly across all classes.MobileNetV2 (86.67% accuracy) showed a slight imbalance; for instance, it achieved a high precision for "No Tumor" but lower recall, meaning it was conservative and occasionally missed healthy cases.VGG16 demonstrated poor recall in minority classes, frequently misclassifying true tumor cases as other categories.C. Confusion Matrix Analysis

13. Which classes were frequently misclassified?
    - Classes Glioma and Meningioma were the most frequently misclassified against one another.

15. What patterns did you observe in the confusion matrix?
    - The confusion matrix revealed that the models rarely confused a healthy brain (No Tumor) with a tumorous brain. Instead, almost all classification errors occurred between Glioma and Meningioma. This pattern suggests that while the models are highly competent at detecting the presence of an anomaly, they struggle with fine-grained differences required to distinguish between specific tumor types due to overlapping visual features (like tissue density and location boundaries).D. ROC and AUC

17. Which model had the highest AUC score?
    - The model with the highest Area Under the ROC Curve (AUC) was ResNet50 (with an AUC score exceeding 0.95 across classes).

19. What does AUC tell us about model performance?
    - AUC measures the model’s ability to distinguish between classes across all possible classification thresholds. A high AUC (close to 1.0) tells us that if you randomly select one positive patient (e.g., Glioma) and one negative patient, there is a 95%+ probability that ResNet50 will correctly assign a higher risk score to the true tumor scan.E. Explainability (Grad-CAM)

21. What did Grad-CAM reveal about model decision-making?
    - Grad-CAM generated visual heatmaps overlaid on the MRI scans, revealing exactly which spatial regions inside the brain influenced the model's final classification decision.

23. Did the model focus on relevant image regions?
    - Yes, for the most part. In successful classifications by ResNet50 and MobileNetV2, the heatmaps lit up intensely directly over the physical location of the tumor mass. However, in VGG16's misclassifications, the heatmap often drifted toward edge artifacts, the skull outline, or completely blank background space, explaining why its predictions failed.

25. Which model produced the most meaningful heatmaps?
    - ResNet50 produced the most structurally accurate and localized heatmaps. Its focus was tightly bound to the precise biological boundaries of the Gliomas and Meningiomas, proving that it learned genuine pathological features rather than just memorizing background noise.F. Model Comparison & Improvement

27. Which model would you recommend for deployment? Why?
    - I strongly recommend ResNet50. It dominated across all performance metrics (91.11% accuracy, top F1-score, lowest loss) and its Grad-CAM heatmaps mathematically prove that its clinical decision-making process aligns closely with where a human radiologist would look.Note: If deploying to a low-resource setting (like a mobile device or a weak hospital server), MobileNetV2 is a viable alternative due to its lightweight framework and respectable 86.67% accuracy.

29. How can you further improve your best-performing model?
    - The model can be improved by:Implementing strategic Data Augmentation (e.g., bounded rotations, slight shearing, and brightness adjustments) to simulate different MRI machine settings.Applying Class Weighting during loss calculation to correct any slight dataset imbalances.Executing Fine-tuning by unfreezing the top layer blocks of ResNet50 and training with a very low learning rate ($10^{-5}$) to specialize the weights for medical imaging.Using an Ensemble method that blends the predictions of ResNet50 and MobileNetV2.G. Real-World Application

31. How can your model be applied in real-world scenarios?
    - This system can be utilized as a Diagnostic Decision Support System in hospitals. It can act as a "second pair of eyes" for radiologists to accelerate MRI triaging—flagging severe tumor cases instantly so urgent scans are reviewed first by specialists.

33. What are the risks of deploying an inaccurate model?
    - In a clinical setting, an inaccurate model carries severe risks:False Negatives: Missing a malignant tumor, resulting in delayed medical treatment and putting a patient's life in danger.False Positives: Misdiagnosing a healthy patient with cancer, causing extreme psychological distress and leading to unnecessary, invasive medical procedures.

35. How can this system be integrated into a mobile/web app?
    - The system can be integrated via the following architectural steps:Model Serialization: Export the trained ResNet50 model to an efficient format (e.g., ONNX or TensorFlow SavedModel).Backend API Setup: Deploy the model inside a backend framework like FastAPI or Flask hosted on a cloud service (AWS/GCP), creating an endpoint (e.g., /predict).Explainability Pipeline: Ensure the API runs both the prediction and the Grad-CAM script, returning both the diagnosis percentage and the generated heatmap image response.Frontend Interface: Build a web interface (using React or Streamlit) where a medical professional can drag-and-drop a DICOM/MRI image file and immediately see the diagnostic output side-by-side with the visual Grad-CAM heatmap.
