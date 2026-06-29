*****************Dataset Description — Multimodal Pedagogical Recommendation System*************************

 **Overview**
 
This project uses the public OULAD (Open University Learning Analytics Dataset) to train and evaluate a system for predicting academic risk and generating personalized pedagogical recommendations. The data has been enriched with a synthetically generated  multilingual text corpus (French/Arabic) to simulate forum exchanges, enabling bimodal modeling of learners.

**📊 Source Data**

Attribute  	Description

Name	          OULAD (Open University Learning Analytics Dataset)

Publication  	(https://www.nature.com/articles/sdata2017171?utm_source=researchgate.net&utm_medium=article)

Kaggle	          https://www.kaggle.com/datasets/anlgrbz/student-demographics-online-education-dataoulad

License	         Creative Commons Attribution 4.0 International (CC BY 4.0)


**📁 OULAD Dataset Structure**

The dataset consists of multiple relational CSV files:

File	Description	Rows

studentInfo.csv	Student demographics and final results	32,593

studentVle.csv	VLE interaction logs (clicks, dates, activities)	10,655,280


vle.csv	VLE resource descriptions (activity types)	6,364
studentAssessment.csv	Assessment scores	173,912

assessments.csv	Assessment descriptions (dates, weights)	206

courses.csv	Course module information	7

studentRegistration.csv	Module registration dates	—

**👩‍🎓 Student Population**

Characteristic	Value

Total students	32,593

Number of modules	7 (AAA, BBB, CCC, DDD, EEE, FFF, GGG)

Observation period	Relative days [-30, +300]

Dropout rate	31.16%

Success rate (Pass/Distinction)	47.2%

Students with VLE activity	29,228 (89.7%)

*********🧠 Enrichment: Synthetic Text Corpus***********

Since no authentic forum messages are available in OULAD, we generated a corpus of 81,714 messages based solely on students' behavioral features to simulate forum interactions.

***Generated Corpus Characteristics***

Attribute	          Value

Total messages	    81,714

Students with messages	29,228 (89.7% of total)

Messages per student (average)	2.8

Languages	French, Arabic, Code-switching

Emotion lexicon	4 categories: frustration, confusion, motivation, anxiety (Pekrun)

Arabic weighting	× 1.5 (to compensate for semantic density)

Semantic model	XLM‑RoBERTa‑base → 768‑dim embeddings

Example Generated Message
"J'ai du mal à suivre, besoin d'aide supplémentaire. ما فهمت الدرس زين."

**🛠️ Preprocessing & Representations**

**1. Behavioral Data**
Daily aggregation of VLE logs

Sliding window sequencing of 30 days

Log‑normalization of clicks

Ordinal encoding of activity types (resource, forum, quiz, etc.)

Zero‑imputation for students without VLE activity (3,365 cases)

***2. Textual Data**

Minimal cleaning (URL removal, mentions, extra spaces)

Bilingual emotion detection using a custom lexicon

Tokenization and embedding extraction with XLM‑RoBERTa ([CLS] token)

Student‑level aggregation: average of embeddings + 7 numerical metrics (length, questions, Arabic presence, etc.)

3. Final Bimodal Profile
   
Each student is represented by a bimodal vector:

Modality	Dimension	Source

Behavioral (LSTM)	32	BiLSTM output on 30‑day sequences

Textual (Affective)	775	768 (XLM‑R) + 7 numerical features

**csv textual link** :  (https://drive.google.com/drive/folders/1yqiq1thnu2hZv58lwoowxfnN-GsnrSq0?usp=sharing)

📌 License & Usage
OULAD is distributed under the Creative Commons Attribution 4.0 International (CC BY 4.0) license.

The generated synthetic text corpus and derived embeddings are released under the same license, with explicit mention of their synthetic nature and research purpose.

