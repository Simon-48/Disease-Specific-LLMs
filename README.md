# Disease-Specific-LLMs

## An Approach to Convert Tabular Clinical Records into Clinical Texts for Training Disease-Specific LLMs Effectively

The key dataset of this study is from the National Institute of Cancer Research and Hospital (NICRH) on sarcoma cancer. As this is a private dataset, its information is not disclosed. Instead, information from a few public datasets—such as the UCI Heart Disease, UCI Heart Failure Clinical Records, and UCI Chronic Kidney Disease datasets—is provided. Kindly check the 'Results.docx' uploaded.

In this study, heart patient data from the UCI Heart Disease dataset were utilized. This data was originally in tabular format, similar to what is typically found in a structured, tabular clinical dataset or Electronic Health Record (EHR)-derived tabular dataset. However, large language models (LLMs) such as GPT perform optimally with text-based input rather than tabular data. This introduced two primary challenges:

    1. The data was in a tabular format, which is not commonly used with transformer-based models like GPT.
    2. The dataset contained very few heart disease cases, making it difficult to train an effective model.
   
The key advantage of employing a language model like GPT over traditional machine learning models or standard neural networks lies in its dual capability. Traditional models make predictions based solely on statistical patterns and observed probabilities within the data. While often effective, such models typically fail to capture the clinical significance behind categorical features, particularly in medical datasets where each category (e.g., “normal,” “abnormal,” “present,” “not present”) conveys nuanced meaning. In contrast, GPT models are capable of understanding clinical context in a manner similar to a healthcare expert while also learning underlying statistical relationships. This combination of semantic understanding and statistical reasoning renders GPT models especially powerful for healthcare applications, where both interpretability and domain knowledge are critical.

The creation of synthetic examples for heart disease prediction poses additional difficulties, especially when the dataset includes numerous categorical features (such as "yes"/"no" or "normal"/"abnormal") with significant clinical implications. Common techniques such as SMOTE, ADASYN, and ENN are well-suited for numerical data but often fail to effectively handle categorical medical data. This limitation impedes the improvement of model performance when real heart disease data is scarce.
To address this, a table-to-text method was developed. Initially, the tabular data was converted into short clinical-style text, resembling the format a physician might use (you can check the converted data in 'Results.docx'). Subsequently, a GPT-based model (GPT4) was employed to generate more realistic and medically accurate examples by paraphrasing existing samples from heart disease patients (you can check the synthetic paraphrased data in 'Results.docx').

This approach preserves the clinical meaning while generating new examples (as it does not alter any values or labels, but rather paraphrases the given text), a feat that traditional methods for creating synthetic data for categorical features, such as SMOTE-NC, CTGAN, TVAE, and CopulaGAN, often struggle to achieve. These alternative techniques either fail to capture the clinical context adequately or generate samples that are less meaningful when dealing with categorical medical features.

Following the generation of realistic medical text samples, a GPT2 model was fine-tuned using the short texts. The objective was to assess whether the model could accurately predict the presence of heart disease in new patients, and the model demonstrated strong performance, even when trained on limited data.
All GPT models used in this study were obtained from Hugging Face’s library of pre-trained models. The findings demonstrate that LLMs can be adapted to handle medical tabular data by transforming it into text, thereby enhancing the model's ability to learn clinically relevant patterns associated with heart disease.
Additionally, this approach was compared to a simpler method in which tabular data was converted into a sequential input format — listing feature values in order, without converting them into clinical-style text. While this method rendered the data compatible with transformer models, performance was suboptimal. Transformer-based models struggled to capture the relationships and clinical significance embedded in plain sequences of numbers or categories.

In contrast, the table-to-clinical-text approach enabled the GPT model to learn both the semantic and clinical context of each feature. This resulted in significantly improved performance and generalization, particularly for the underrepresented heart disease class.

To evaluate the generalizability of the proposed method, it was also applied to the UCI Heart Failure Clinical Records dataset and the UCI Chronic Kidney Disease dataset, with consistent results obtained across all datasets.

Improvements:
  
      1.	Developed a more effective approach to utilizing structured, tabular clinical datasets or EHR-derived tabular data within transformer-based Large Language Models (LLMs), addressing the initial incompatibility of LLMs with tabular data formats.
      
      2.	Proposed a paraphrasing-based method to correct class imbalance in structured, tabular clinical datasets or EHR-derived data by preserving the underlying medical semantics, especially for categorical features where each category carries distinct medical significance, making synthetic data generation challenging.

**The codes are private.**
