🧠 Approach
4 strong Arabic language models are used:

UBC‑NLP/MARBERT

aubmindlab/bert-large-arabertv02

FacebookAI/xlm-roberta-base

CAMeL‑Lab/bert-base-arabic-camelbert-mix

5‑fold Stratified K‑Fold on the combined training+validation data (1024 samples) to make full use of all labeled data.

Weighted loss (class weights computed per fold) to handle mild class imbalance.

Ensemble by averaging prediction probabilities over all models and folds.

📊 Results
On the evaluation set (181 samples) the ensemble achieves:

Accuracy: 97.79%

Macro F1: 0.9777

Per‑class F1:

pro: 0.9920

against: 0.9672

neutral: 0.9739

🗂️ Data
The dataset consists of three Excel files:

Subtask_B_train.xlsx – training set with labels

Subtask_B_eval_labeled.xlsx – evaluation set with labels (used for validation during training)

_Subtask_B_test_noLabel.xlsx – test set without labels (predictions are generated for this set)

Each file contains columns: sentence, topic, and (for labeled sets) label or prediction.

🚀 Usage
Install dependencies (see requirements.txt or run the first cell of the notebook):

bash
pip install transformers torch pandas scikit-learn openpyxl sentencepiece
Update file paths in the second cell of the notebook to point to your local copies of the data files.

Run the notebook – training and evaluation will be performed automatically.

Output – predictions on the test set are saved to results/predictions.csv and also zipped as predictions.zip.
📌 Notes
Training uses bfloat16 (bf16) to speed up training on compatible GPUs.

The notebook is designed to run on Kaggle (with GPU enabled), but can be adapted to any environment with CUDA support.

Early stopping is not used because save_strategy="no" saves disk space; the full 5 epochs are run.

🤝 Acknowledgements
Models from Hugging Face Hub by UBC‑NLP, aubmindlab, FacebookAI, and CAMeL‑Lab.

Nakba dataset provided by the competition organisers.
