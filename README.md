# Exercise Recognition and Posture Feedback

## Introduction

In recent years, the fitness industry has increasingly integrated technology to enhance workout experiences and improve health outcomes. Our project, **Exercise Recognition and Posture Feedback**, aims to develop an automated system to accurately recognize exercise poses from videos and provide real-time feedback on posture correctness.

This project addresses two critical needs in the fitness industry:
1. Ensuring proper form to prevent injuries.
2. Maximizing workout effectiveness.

Given the limited availability and high costs associated with personal trainers, our project offers a cost-effective and accessible alternative for users seeking workout guidance.

Deep learning is a suitable approach for this task as it excels at pattern recognition through training on large datasets. By leveraging deep learning models, the project classifies various exercises based on body poses and detects common form errors, providing users with feedback to enhance their workouts.

![image](https://github.com/user-attachments/assets/0405a568-870e-4aa3-ab29-f1d2cad1c77c)
**Figure 1: Overview of the inputs and outputs of our model**  

## Background & Related Work

Wearable technology and external sensors have traditionally been used for exercise recognition, but these methods reduced user experience. With advancements in computer vision, exercise recognition models can now track physical movements, identify exercises and their repetitions, analyze movements, determine correctness, and provide real-time feedback.

Existing platforms like **Kemtai, Peloton, Xtra, GymCam, and Sency AI** offer exercise recognition but focus on different aspects such as physiotherapy, personal training, musculoskeletal screening, and tracking multiple people’s exercises. Our project aims to provide an efficient and accessible alternative.

## Data Processing

We utilized various data sources, including structured datasets from **Kaggle** and exercise clips from **YouTube**. To ensure quality and consistency, the following preprocessing steps were applied:

1. **Manual Review & Segmentation:**
   - Videos were reviewed and cleaned, discarding those with poor visibility.
   - 100 videos of good form and 50 videos of bad form were retained for each exercise.

2. **Duplication:**
   - Bad form videos were duplicated to create an equal number of good and bad examples (100 each per exercise).

3. **Augmentation:**
   - Applied rotations, flips, stretching, brightness adjustments, and noise to enhance dataset diversity, expanding it to **500 videos of good and bad form per exercise**.

4. **Labeling:**
   - Videos were labeled accordingly (e.g., `deadlift_good1` or `deadlift_bad1`).
   - Organized into a structured dataset.

5. **Freeze Frame Extraction:**
   - Static images were extracted at regular intervals from videos to convert dynamic data into static images for training.

![image](https://github.com/user-attachments/assets/e2ea2663-4c74-4478-8c1d-f262b2ea8bbc)
**Figure 2: Number of videos per exercise**  

## Model Architecture

To accurately recognize and classify exercise poses, we implemented a **hybrid CNN-LSTM model**:
- **CNN (Convolutional Neural Network):** Extracts spatial features from frames.
- **LSTM (Long Short-Term Memory):** Captures temporal dependencies for motion analysis.

Since we have not yet covered **RNNs in our lectures**, only the CNN part has been implemented so far.

![image](https://github.com/user-attachments/assets/fe53f8f6-4cb2-4cec-bb1f-4117f664b546)
**Figure 3: CNN-LSTM model architecture**  

## Baseline Model

For comparison, a **Random Forest (RF) model** was trained as a baseline classifier.
- Trained on extracted features.
- Used 32 trees with weighted balancing.
- Achieved **55% test accuracy**, indicating its limitations for complex, imbalanced datasets.

## Results

### Quantitative Results

The model was trained to:
1. **Classify the type of exercise**.
2. **Assess whether the exercise form was good or bad**.

![image](https://github.com/user-attachments/assets/3e374111-7cba-4b1e-b6d7-8e2781c0f49e)
**Figure 4: Model accuracy plot**  


- **Exercise classification accuracy:** ~81% (test dataset).
- **Form assessment accuracy:** 61% (test dataset).

**Confusion Matrices:**
![image](https://github.com/user-attachments/assets/fc5fa7fd-73fa-4faa-ae8a-d556fe1556c9)
- **Figure 5: Exercise classification confusion matrix**  
![image](https://github.com/user-attachments/assets/1818b202-ebc8-40e1-95e4-962afc712220)
- **Figure 6: Form assessment confusion matrix**  

### Qualitative Results

- Model successfully classified most exercises but sometimes misclassified **planks as pull-ups**.
- Struggled with subtle posture differences for form assessment.

![image](https://github.com/user-attachments/assets/5db7c7c6-46ce-4049-9872-de674bdd83f5)
**Figure 7: Correctly classified exercises**  
![image](https://github.com/user-attachments/assets/83c165e4-83b1-4b67-846e-8eeff6c852d4)
**Figure 8: Pull-up misclassified as plank**  
![image](https://github.com/user-attachments/assets/d244abe4-6277-4968-a999-75a43d218389)
**Figure 9: Bad plank misclassified as good**  

## Evaluation

The model was tested on unseen videos sourced from **YouTube, Kaggle, TikTok, and real-world recordings**.

### Case Study: Pull-Up Evaluation

- One test video showed a **left-leaning pull-up (incorrect form)**.
- Another test video showed a **proper pull-up**.
- The model correctly classified both and assessed form accurately.

![image](https://github.com/user-attachments/assets/4fef46a6-ca1c-4e6a-b0a7-c0d740edbde7)
**Figure 10: Pull-up assessment results**  

## Discussion

### Classification
- Model performed well with **90% accuracy**.
- Robust enough to classify various exercises reliably.

### Form Assessment
- **85% accuracy** suggests difficulty in detecting subtle form differences.
- More professional guidance in dataset labeling could improve robustness.

![image](https://github.com/user-attachments/assets/eda12907-3d0f-46a8-a8ec-0ce15e0af58a)
**Figure 11: Incorrect form assessment**  

## Observations & Limitations

### Unusual Misclassification
- The model sometimes confused planks with pull-ups due to **camera angles and elbow positioning**.
![image](https://github.com/user-attachments/assets/d952a43d-0c2c-4fa2-820e-48601a48e677)
**Figure 12: Rotated pull-up vs plank**  

### Robust Classification
- Surprisingly, the model distinguished **deadlifts from barbell curls** despite similar arm movements and added equipment noise.

## Ethical Considerations

1. **Biased Assessment**:
   - Variability in labelling "good" and "bad" postures could lead to inconsistent feedback.
2. **Over-Reliance on AI Feedback**:
   - Users might depend entirely on the model, ignoring pain or discomfort.

## Future Improvements

- Improve dataset quality with **expert-labeled posture data**.
- Implement **advanced feature extraction techniques** to enhance assessment accuracy.
- Expand the dataset with **more diverse body types and workout settings**.
- Fine-tune **LSTM integration** for improved temporal modeling.

## References


