# Point of View (POV) of Message Conversion Dataset
Virtual assistants (VAs) tend to be literal in their delivery of messages. Most likely, if you ask them to deliver a message, the VAs either send a recorded message or a literal transcription to the receiver. To make incremental improvement towards a virtual assistant that you may speak to conversationally and naturally, we have provided the data necessary to build AI systems that can convert the point of view of messages spoken to virtual assistants.

If a sender asks the virtual assistant to relay a message to a receiver, the virtual assistant converts the message to VA's perspective and composes a conversational relay message. i.e.

- **Sender (isabelle):** ask nick if he wants anything from trader joe's
- **VA to receiver (nick):** hi nick, isabelle wants to know if you want anything from trader joe's? 

Our public release of the dataset contains parallel corpus of input and output utterances as such. This release also contains surveys used for data collection and human evaluation on resulting model output covered in our paper.

### Table of Content
1. [Data](#data)
2. [Surveys](#surveys)
3. [Human Evaluation](#human-evaluation)
4. [Citation](#citation)
5. [Acknowlegements](#acknowledgements)

For more detailed explanation on the problem statement, the [Surveys](#surveys), or metrics introduced in [Human Evaluation](#human-evaluation), please refer to our [paper](ARXIV LINK TO BE ADDED). For future work involving this dataset, please refer to our licenses and code of conduct.


## Data 

The dataset contains parallel corpus of input (`input` column) message and POV converted messages (`output` column). An example of a pair is
```tell @CN@ that i'll be late [\t] hi @CN@, @SCN@ would like you to know that they'll be late.``` The input and pov-converted output pair is tab separated. `@CN@` tag is a placeholder for the contact name (receiver) and `@SCN@` tag is a placeholder for source contact name (sender).

The total dataset has 46563 pairs. This data is then test/train/dev split into 6985 pairs/32594 pairs/6985 pairs.


## Surveys 
This release also contains the surveys used to collect our data. Our primary source of data was Amazon-internal associates and crowdsourcing on Amazon Mechanical Turk. The surveys are in HTML format compatible for Mturk.

The survey contains `stmt.html`, `askin.html`, `askyn.html`, `do.html`, `req.html`, and `askwh.html`. To better control the data collection process and in loose accordance to the original rule-based approach for generating conversion transformation, the input utterances were gathered by input message categories. 

| Type of Input | Description | Example |
| ---- | ---- | ---- |
| Statement | a statement made by a sender to receiver | tell priya that i'll be late |
| AskYN | a yes/no question made by a sender to receiver; i.e. often looks like *ask if* | ask priya if they'll be late |
| AskIN | a vague question *about* a subject | ask priya about the apartment lease |
| AskWH | a reference-specified question involving wh-interrogatives | ask priya what time is the meeting |
| Request | a request for action to be performed by a sender to receiver | ask priya to please get back to me |
| Do | a question or a statement involving the auxiliary verb do; Note: this category is simply a survey category to add more variety in samples. The gathered data can belong in any of the categories above | ask priya did she like her present? |


## Human Evaluation

In our paper, we've used various ML models to perform this task. A rule-based model was initially developed to further investigate the problem statement, and then neural encoder-decoder models were later used. For human evaluation, we've evaluated output of rule-based model, T5 and CopyNet trained on this corpus.

For each output, 3 associates have evaluated faithfulness and naturalness, with faithfulness as a binary metric and naturalness as a semi-binary metric. Faithfulness evaluates whether or not the converted message preserved the content of the input message accurately. Naturalness evaluates how natural the converted utterance sounded. Since naturalness encompasses tolerance for grammaticality, locality, and personal inclinations, naturalness was evaluated on a scale of 1 to 4.

- 1 - unintelligible, un-english
- 2 - poor; the construction is poor, but not completely unintelligible
- 3 - acceptable; the sentence is acceptable, but there's something that just doesn't feel comfortable.
- 4 - perfect

Then, this metric was converted to unnatural (1 or 2) or natural (3 or 4).

### Brief Human Evaluation Results

| Model | Annotator Agreement (Faithfulness) | Annotator Agreement (Naturalness) | Faithfulness Model Accuracy | Naturalness Model Accuracy |
| --- | --- | --- | --- | --- |
| CopyNet | 0.94 | 0.89 | 0.94 | 0.97 |
| T5 | 0.86 | 0.88 | 0.98 | 0.98 |
| Rule-based Model | 0.72 | 0.71 | 0.85 | 0.76 |

As additional data, CopyNet's human evaluation results are included in `human-evaluation` folder.

## Citation 
```
@inproceedings{Lee2020,
  author={Isabelle G. Lee and Vera Zu and Sai Srujana Buddi and Dennis Liang and Purva Kulkarni and Jack Fitzgerald},
  title={{Converting the Point of View of Messages Spoken to Virtual Assistants}},
  year=2020,
  booktitle={Proc. EMNLP 2020},
  doi={to-be-added},
  url={to-be-added}
}
```

```
Lee, I.G., et al. "Converting the Point of View of Messages Spoken to Virtual Assistants"
```

## Acknowledgements 
We'd like to thank Steven Spielberg P. for coordinating our efforts and for early contribution, and we'd like to thank Adrien Carre and Minh Nguyen on coordinating with associates for the dataset and human evaluation of model output.


## License
Under CDLA-Sharing 1.0 License
