# GCRC
  GCRC: A New Challenging MRC Dataset from Gaokao Chinese for Explainable Evaluation

### Introduction
  Currently, machine reading comprehension models have made exciting progress, driven by a large number of publicly available data sets. However, the real language comprehension capabilities of models are far from what people expect, and most of the data sets provide black-box evaluations that fail to diagnose whether the system is based on correct reasoning processes. In order to alleviate these problems and promote machine intelligence to humanoid intelligence, Shanxi University focuses on the more diverse and challenging reading comprehension tasks of the college entrance examination, and attempts to evaluate machine intelligence effectively and practically based on standardized human tests. We collected gaokao reading comprehension test questions in the past 10 years and constructed a datasets which is GCRC(A New MRC Dataset from Gaokao Chinese for Explainable Evaluation) containing more than 5000 texts and more than 8,700 multiple-choice questions (about 15,000 options). The datasets is annotated three kinds of information: the sentence level support fact, interference item’s error cause and the reasoning skills required to answer questions. Related experiments show that this datasets is more challenging, which is very useful for diagnosing system limitations in an interpretable manner, and will help researchers develop new machine learning and reasoning methods to solve these challenging problems in the future.

### Leaderboard
[GCRC Leaderboard for Explainable Evaluation ](http://cuge.baai.ac.cn/#/dataset?id=22&name=GCRC)

### Paper
[GCRC: A New Challenging MRC Dataset from Gaokao Chinese for Explainable Evaluation](https://aclanthology.org/2021.findings-acl.113.pdf). ACL 2021 Findings.

### Data Size
Train：6,994 questions；Dev：863 questions；Test：862  questions

### Data Format
Each instance is composed of 
id (id, a string),
title (title, a string), 
passage (passage, a string), 
question(question, a string), 
options (options, a list, representing the contents of A, B, C, and D, respectively), 
evidences (evidences, a list, representing the contents of the supporting sentence in the original text of A, B, C and D, respectively),
reasoning_ability(reasoning_ability, a list，representing  the reasoning ability required to answer questions of A, B, C and D, respectively),
error_type (error_type, a list, representing the Error reason of  A, B, C and D, respectively),
answer(answer,a string).

### Example
```json
{
  "id": "gcrc_4916_8172", 
  "title": "我们需要怎样的科学素养", 
  "passage": "第八次中国公民科学素养调查显示，2010年，我国具备...激励科技创新、促进创新型国家建设，我们任重道远。", 
  "question": "下列对“我们需要怎样的科学素养”的概括，不正确的一项是", 
  "options":  [
    "科学素养是一项基本公民素质，公民科学素养可以从科学知识、科学方法和科学精神三个方面来衡量。",
    "不仅需要掌握足够的科学知识、科学方法，更需要具备学习、理解、表达、参与和决策科学事务的能力。",
    "应该明白科学技术需要控制，期望科学技术解决哪些问题，希望所纳的税费使用于科学技术的哪些方面。", 
    "需要具备科学的思维和科学的精神，对科学技术能持怀疑态度，对于媒体信息具有质疑精神和过滤功能。"
  ],
  "evidences": [
    ["公民科学素养可以从三个方面衡量：科学知识、科学方法和科学精神。", "在“建设创新型国家”的语境中，科学素养作为一项基本公民素质的重要性不言而喻。"],
    ["一个具备科学素养的公民，不仅应该掌握足够的科学知识、科学方法，更需要强调科学的思维、科学的精神，理性认识科技应用到社会中可能产生的影响，进而具备学习、理解、表达、参与和决策科学事务的能力。"], 
    ["西方发达国家不仅测试公众对科学技术与社会、经济、文化等各方面关系的看法，更考察公众对科学技术是否持怀疑态度，是否认为科学技术需要控制，期望科学技术解决哪些问题，希望所纳的税费使用于科学技术的哪些方面等。"], 
    ["甚至还有国家专门测试公众对于媒体信息是否具有质疑精神和过滤功能。", "西方发达国家不仅测试公众对科学技术与社会、经济、文化等各方面关系的看法，更考察公众对科学技术是否持怀疑态度，是否认为科学技术需要控制，期望科学技术解决哪些问题，希望所纳的税费使用于科学技术的哪些方面等。"]
   ],
  "error_type": ["E", "", "", ""],
  "answer": "A",
}
```

### Evaluation Code
The prediction result needs to be consistent with the format of the training set.
```shell
python eval.py prediction_file test_private_file
```
Participants are required to complete the following tasks:
Task 1: Output the answer to the question.
Task 2: Output the sentence-level supporting facts（SFs） that support the answer to the question, that is, the original supporting sentences for each option.
Task 3: Output the error cause of the interference option. There are 7 reasons for the error in this evaluation: 1) Wrong details; 2) Wrong temporal properties; 3) Wrong subject-predicate-object triple relationship; 4) Wrong necessary and sufficient conditions; 5) Wrong causality; 6) Irrelevant to the question; 7) Irrelevant to the article.
The evaluation metrics are Task1_Acc, Task2_F1，Task3_Acc（The accuracy of error reason identification）,and the output is in dictionary format.
```shell
return {"Task1_Acc":_, " Task2_F1":_, "Task3_Acc":_}
```

### Institutions
[Shanxi University](https://github.com/SXUNLP)

### Citation
Please kindly cite our paper if the work is helpful.
```bibtex
@inproceedings{tan-etal-2021-gcrc,
    title = "{GCRC}: A New Challenging {MRC} Dataset from {G}aokao {C}hinese for Explainable Evaluation",
    author = "Tan, Hongye  and
      Wang, Xiaoyue  and
      Ji, Yu  and
      Li, Ru  and
      Li, Xiaoli  and
      Hu, Zhiwei  and
      Zhao, Yunxiao  and
      Han, Xiaoqi",
    booktitle = "Findings of the Association for Computational Linguistics: ACL-IJCNLP 2021",
    month = aug,
    year = "2021",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2021.findings-acl.113",
    doi = "10.18653/v1/2021.findings-acl.113",
    pages = "1319--1330",
}
```
