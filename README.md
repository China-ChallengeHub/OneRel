## OneRel: Joint Entity and Relation Extraction with One Model in One Step

This repository contians the source code and datasets for the paper: **OneRel: Joint Entity and Relation Extraction with One Model in One Step**, Yu-Ming Shang, Heyan Huang and Xian-Ling Mao, AAAI-2022.

## Motivation

Most existing joint entity and relaiton extraction methods suffer from the problems of cascading errors and redundant information. We think that the fundamental reason for the problems is that the decomposition-based paradigm ignores an important property of a triple -- its head entity, relation and tail entity are interdependent and indivisible. In other words, it is unreliable to extract one element without fully perceiving the information of the other two elements. Therefore, this paper propose a novel perspective for joint entity and relation extraction, that is, transforming the task into a triple classification problem, making it possible to capture the information of head entities, relations and tail entities at the same time.

## Relation-Specific Horns Tagging

In order to decode entities and relations from the output matrix accurately and efficiently, we introduce a relation-specific horns tagging, as shown in the figure. So, for each relation, the spans of head entities are spliced from "HB-TE" to "HE-TE"; the spans of tail entities are spliced from "HB-TB" to "HB-TE"; and two paired entities share the same "HB-TE".

![tagging](/img/tagging.png)

## Usage

1. **Environment**
   ```shell
   conda create -n your_env_name python=3.8
   conda activate your_env_name
   cd OneRel
   pip install -r requirements.txt
   ```

2. **The pre-trained BERT**

    The pre-trained BERT (bert-base-cased) will be downloaded automatically after running the code. Also, you can manually download the pre-trained BERT model and decompress it under `./pre_trained_bert`.


3. **Train the model (take NYT as an example)**

    Modify the second dim of `batch_triple_matrix` in `data_loader.py` to the number of relations, and run

    ```shell
    python train.py --dataset=NYT --batch_size=8 --rel_num=24 
    ```
    The model weights with best performance on dev dataset will be stored in `checkpoint/NYT/`

4. **Evaluate on the test set (take NYT as an example)**

    Modify the `model_name` (line 48) to the name of the saved model, and run 
    ```shell
    python test.py --dataset=NYT --rel_num=24
    ```

    The extracted results will be save in `result/NYT`.

## Results
To reproduce the performance of the paper, please download our model states [here](https://drive.google.com/drive/folders/1VKd0Y3kSXQ8Vf8W7ZudEUEn2FNx6nSLr?usp=sharing).


## **Acknowledgment**

I followed the previous work of [longlongman](https://github.com/longlongman/CasRel-pytorch-reimplement) and [weizhepei](https://github.com/weizhepei/CasRel). 

So, I would like to express my sincere thanks to them. 



