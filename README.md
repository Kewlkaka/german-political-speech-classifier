# German Political Speech Classifier
## Table of Contents
1. Overview
2. Project Highlights
3. Data Sources and Preprocessing
4. Model Architecture
5. Training and Evaluation
6. How to Use (Demo / Interface)
7. Results
8. Future Work

## 1. Overview
This project aims to classify political speeches based on their content to identify the speaker's political orientation (e.g., liberal, conservative).
### Motivation:
- To understand political trends and sentiments through automated analysis of parliamentary speech data.
- It provides researchers, analysts, and policymakers with insights into political rhetoric and discourse alignment.

### Summary:
- The project processes multiple CSV datasets containing political speeches and metadata, merges them, and uses a BERT-based transformer model for classification. A Gradio-based web app allows users to input speeches and obtain predictions in real-time.

## 2. Project Highlights
- Hugging Face Transformers: Leverages pre-trained BERT ("bert-base-german-cased") for sequence classification.
- Data Integration: Combines datasets from different sources, handling missing values and ensuring consistent formatting.
- Scalable Pipeline: Implements train/test splitting, tokenization, and PyTorch dataset integration.
- Interactive Demo: Provides a Gradio-based web app for live inference.
- Early Stopping: Includes early stopping for efficient model training.

## 3. Data Sources and Preprocessing

### Data Sources:
- all_mps_mapping.csv: Contains metadata such as MPID, state, period, party, and political orientation.
- Bundestag, Bayern, Berlin, NordrheinWestfalen: Contains speech data from parliamentary sessions with attributes such as date, MPID, party, constituency, and speech content.

### Preprocessing Steps:
- Data Cleaning: Removed rows with missing values in critical columns like Speech and Political Orientation.
- Data Merging: Merged datasets with all_mps_mapping.csv on the MPID column to include political orientation.
- Label Encoding: Converted Political Orientation into numerical labels using LabelEncoder.
- Final Dataset Shape: After preprocessing, the dataset contained 2,429 rows and 5 columns (MPID, Party, Date, Speech, and Political Orientation).

## 4. Model Architecture

### Transformer Model:
- Base Model: bert-base-german-cased (BERT variant pre-trained on German text).
- Modifications: Added a classification head with num_labels equal to the number of unique political orientations.

### Tokenization:
- Used Hugging Face's BertTokenizerFast with truncation and padding up to a maximum length of 512 tokens.

## 5. Training & Evaluation

### Training Setup:
- Train/Test Split: 80/20 stratified split to ensure balanced class distribution.
- Training Arguments:
   - Batch size: 16
   - Learning rate: 5e-5
   - Epochs: 3
   - Early stopping after 2 rounds of no improvement.

### Evaluation Metrics:
- Precision, Recall, F1-Score (macro and weighted averages).
- Confusion matrix for detailed performance analysis.

Class | Precision | Recall | F1-Score | Support 
--- | --- | --- | --- |--- |
Communist | 1.00 | 0.33 | 0.50 | 6
--- | --- | --- | --- |--- |
Conservative | 0.90 | 0.87 | 0.88 | 142
--- | --- | --- | --- |--- |
Liberal | 0.78 | 0.95 | 0.85 | 93
--- | --- | --- | --- |--- |
Right-Wing Populist | 1.00 | 0.42 | 0.59 | 19
--- | --- | --- | --- |--- |
Social Democratic | 0.94 | 0.94 | 0.94 | 226

- Overall Accuracy: 89%

## 6. How to Use (Demo / Interface)

- Demo: A Gradio web app provides a simple interface for inference. Users input a speech, and the app predicts its political orientation.
- Instructions: Clone the repository and install dependencies (see Requirements). Run code to attain model, use gradio to launch.

## 7. Results

### Key Achievements:
  - High classification accuracy for major political orientations.
  - Clear differentiation between social democratic and liberal ideologies.

### Confusion Points:
  - Low recall for classes with minimal support (e.g., communist, right-wing populist).

## 8. Future Work
- Data Augmentation: Expand dataset to address class imbalance.
- Fine-Tuning: Explore advanced transformer architectures like RoBERTa.
- Multilingual Support: Extend to speeches in other languages.
- Explainability: Implement SHAP or LIME for model interpretation.
