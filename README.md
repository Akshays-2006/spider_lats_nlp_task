# spider_lats_nlp_task

## Current Progress
- Created the transformer block from scratch
- Using a Encoder block with 3 transformer blocks with 3 heads for multi-head attention and two heads one for act and one for emmotion classification
- Used CE Loss for training
- Embedding Size : 300
- Used fastext cc 300 bin pre trained embedding
- From the Daily Dialog Dataset each utterance was separated which increase the size of the dataset allowing more corpus to train on
- Also each data point was passed with the previous utterances as context and used "speaker 1" and "speaker 2" tokens to separate each utterance
- Achieved Best **Emotion Accuracy of 65.21%** and **act accuracy of 55.19%**
- Achieved Best **Emotion F1 Macro Score of 0.19** and **Act F1 Macro Score of 0.45**

## Future Improvements
- Implementing Custom Trainable Embeddings so it'll be able to learn the semantic meaning better for this specific case
- Implement Emotion Based Attention Layer like in "Emotion-Aware RoBERTa enhanced with emotion-specific attention" to attend to the emotions sppecific words better
- Experimenting with Decoupled training (Training the model first and then freezing the backbone and training the classifier alone again)
- Experiment with Logit Adjustment
- Speaker Embedding

| Experiment | Best Act Macro F1 Score | Best Emotion Macro F1 Score |  Inference  |
|----------  |----------               |----------                   |-------------|
| Basic Bottomline  | 0.379  | 0.202  | Good/Decent Accuracy But Bad F1 Score because of class imbalance which has to be handled |
| Inverse Frequency Based Class Weights  | 0.423  | 0.1913  | Decent Improvement in Act F1 Score whereas small dip in Emotion F1 Score But most importantly Training was highly unstable |
| Log Class Weights | 0.458 | 0.196 | A slight Improvement in Act F1 score and training was veryy stable compared to plain inverse frequency Class weights |


## Experiments

### Experiment 1

**Best Test F1 --> F1 Act : 0.3798332931463562
F1 Emotion : 0.20281247330023966**

**Best Test Acc --> Act acc : 57.09%    Emotion Acc : 85.92%**
**Best Training Acc --> Act acc : 55.39%   Emotion Acc : 85.29%**

- No Class balancing
- Cross Entropy Loss (weightage::1:1)
- lr=3e-5
- 3 trans block with 3 heads each
- embedding size:300
- tokenizer & emb: fasttext cc 300 bin

#### Loss,Accuracy Vs Epoches Graph
<img width="644" height="455" alt="Pasted image 20251225174831" src="https://github.com/user-attachments/assets/b4fea01a-1f28-4daa-8f75-9f75d242dc9e" />

### Experiment 2

**Best Test F1 --> F1 Act : 0.4231397687354939
F1 Emotion : 0.19139300309615653**

**Best Test Acc --> Act acc : 49.73199%    Emotion Acc : 44.09585%**
**Best Training Acc --> Act acc : 48.68905 %   Emotion Acc : 28.75814%**

- Inverse frequency Class Weight Balancing                                                                             
- Cross Entropy Loss (weightage::1:1)
- lr=3e-5
- 3 trans block with 3 heads each
- embedding size:300
- tokenizer & emb: fasttext cc 300 bin

#### Loss,Accuracy Vs Epoches Graph
<img width="644" height="455" alt="Pasted image 20251227211945" src="https://github.com/user-attachments/assets/25e6a8bf-5a4a-4540-a743-24dc8a971a8e" />


### Experiment 3

**Best Test F1 --> F1 Act : 0.4583626706404825
F1 Emotion : 0.19593726265764175**

**Best Test Acc --> Act acc : 55.19208%    Emotion Acc : 65.21625%**
**Best Training Acc --> Act acc : 53.54929  %   Emotion Acc : 76.89418%**                                                  

- Log-Class Weight Balancing                                                                             
- Cross Entropy Loss (weightage::1:1)
- lr=3e-5
- 3 trans block with 3 heads each
- embedding size:300
- tokenizer & emb: fasttext cc 300 bin

#### Loss,Accuracy Vs Epoches Graph
 <img width="644" height="455" alt="Pasted image 20251227214256" src="https://github.com/user-attachments/assets/be5ed3f5-3fb4-4a76-a2de-fb98ca8d65be" />
