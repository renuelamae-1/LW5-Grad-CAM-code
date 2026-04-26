# LW5-Grad-CAM-code

A. Model Performance

1. Which pre-trained model achieved the highest accuracy? Why?
The model that achieved the highest accuracy was [Model Name, e.g., ResNet50]. This is likely because it has a deeper architecture, allowing it to extract more complex features from the images and generalize better compared to other models.

2. Which model had the lowest performance? What could be the reason?
The lowest-performing model was [Model Name], possibly due to its simpler architecture or limited feature extraction capability. It may also be more prone to underfitting or not well-suited for the dataset used.

3. How did loss values compare across models?
The best-performing model showed the lowest validation loss, indicating better generalization. Models with higher loss values may have struggled to learn patterns effectively or may have overfitted the training data.

B. Evaluation Metrics

4. Why is accuracy not enough to evaluate a model?
Accuracy alone can be misleading, especially when the dataset is imbalanced. A model may achieve high accuracy by predicting the majority class but fail to correctly identify minority classes.

5. Which model had the best F1-score? What does it indicate?
The model with the highest F1-score was [Model Name]. This indicates a good balance between precision and recall, meaning the model performs well in both identifying correct positives and minimizing false predictions.

6. How did Precision and Recall differ across models?
Some models had higher precision but lower recall, meaning they were more conservative in predictions. Others had higher recall but lower precision, meaning they detected more positives but with more false alarms.

C. Confusion Matrix Analysis

7. Which classes were frequently misclassified?
Classes such as [Class A] and [Class B] were frequently misclassified, likely because they share similar visual features.

8. What patterns did you observe in the confusion matrix?
The confusion matrix showed that most errors occurred between visually similar classes, while distinct classes were classified correctly. This suggests that the model struggles with fine-grained differences.

D. ROC and AUC

9. Which model had the highest AUC score?
The model with the highest AUC score was [Model Name], indicating better discrimination between classes.

10. What does AUC tell us about model performance?
AUC measures the model’s ability to distinguish between classes. A higher AUC means the model is better at correctly ranking positive and negative instances across different thresholds.

E. Explainability (Grad-CAM)

11. What did Grad-CAM reveal about model decision-making?
Grad-CAM showed which parts of the image influenced the model’s predictions, helping visualize how the model interprets input data.

12. Did the model focus on relevant image regions?
Yes, the model generally focused on relevant areas, such as [important features, e.g., objects or regions], although some misclassifications showed attention on irrelevant regions.

13. Which model produced the most meaningful heatmaps?
[Model Name] produced the most meaningful heatmaps, indicating it learned more relevant spatial features compared to others.

F. Model Comparison & Improvement

14. Which model would you recommend for deployment? Why?
I would recommend [Model Name] because it achieved the best balance of accuracy, F1-score, and AUC, while also showing reliable behavior in the confusion matrix and Grad-CAM analysis.

15. How can you further improve your best-performing model?
The model can be improved by:

Increasing dataset size or balancing classes
Applying data augmentation
Fine-tuning hyperparameters
Using ensemble methods
Training for more epochs with proper regularization
G. Real-World Application

16. How can your model be applied in real-world scenarios?
The model can be used in applications such as automated image classification, medical diagnosis, or object detection systems, depending on the dataset.

17. What are the risks of deploying an inaccurate model?
An inaccurate model can lead to incorrect predictions, which may cause serious consequences such as wrong decisions, loss of trust, or potential harm in critical applications.

18. How can this system be integrated into a mobile/web app?
The system can be integrated by:

Converting the model into a deployable format (e.g., TensorFlow Lite)
Connecting it to a backend API (Flask/Django)
Building a frontend interface where users can upload images and receive predictions
