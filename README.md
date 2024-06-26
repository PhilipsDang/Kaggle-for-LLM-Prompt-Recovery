# Kaggle-for-LLM-Prompt-Recovery
Hi, I'm Philips, an international high school student in Beijing, China, and this is my code for the 2024 Kaggle competition "LLM Prompt Recovery". My final result was a global silver medal, ranking 41 in the world

Competition Overview:
    In recent years, the development of Large Language Models (LLMs) is becoming matured, making the text they generate increasingly difficult to distinguish from human writing. The competition required participants to develop a machine learning model capable of accurately detecting whether an essay was written by a student or an LLM. The competition dataset included essays written by students and articles generated by various LLMs. This competition was a typical binary classification problem, with the evaluation metric being AUC.

Algorithm Descriptions:
1.Training Sample Generation:
a)Prompts Creation: Extensively generate rewriting prompts using ChatGPT.
b)Original Texts: Source open web texts from Hugging Face, filtering longer texts.
c)Text Rewriting: Input texts from steps above into Google's open LLM, gemma-7b-it, to create rewritten text data for training samples.
2.Seq2Seq Model:
a)Preprocessing: Convert prompts from generated samples into embedding vectors for faster training.
b)Training Pipeline: Input original and rewritten texts into deberta-v3-large model, concatenate feature outputs, and train on similarity with actual prompt embeddings.
c)Retrieval Database: Create a large database of prompt embeddings for inference retrieval.
d)Inference: Use the trained model for online inference to predict prompt embeddings and retrieve the most similar prompt text from the database.
3.Phi2 Fine-Tuning Model: Employ an open-source Phi2 fine-tuning model for prediction, focusing on key text segments.
4.Zero-Shot LLM Model: Use the open-source model Mistral-7B-Instruct-v0.2, inputting examples to predict directly.
5.Ensemble Prediction: Combine predictions from the three models by string concatenation for the final result.
Data Files:
prompts_df.csv: Prompts for rewritten texts.
train_clean.parquet: Training data samples.
validation826.csv: Validation set.
