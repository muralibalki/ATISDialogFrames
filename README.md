
# ATIS Dialog Frames

This repository contains the modified ATIS dataset to include Dialog Frames. This dataset is further described in the paper:
* Title: Recursive Template-based Frame Generation for Task Oriented Dialog
* Authors: Rashmi Gangadharaiah and Balakrishnan Narayanaswamy
* Email : {rgangad,muralibn}@amazon.com
* https://www.aclweb.org/anthology/2020.acl-main.186.pdf
* Accepted as a research paper at ACL 2020


If you use this dataset, please cite our paper:
```
@inproceedings{gangadharaiah-narayanaswamy-2020-recursive,
    title = "Recursive Template-based Frame Generation for Task Oriented Dialog",
    author = "Gangadharaiah, Rashmi  and
      Narayanaswamy, Balakrishnan",
    booktitle = "Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics",
    month = jul,
    year = "2020",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/2020.acl-main.186",
    doi = "10.18653/v1/2020.acl-main.186",
    pages = "2059--2064",
    abstract = "The Natural Language Understanding (NLU) component in task oriented dialog systems processes a user{'}s request and converts it into structured information that can be consumed by downstream components such as the Dialog State Tracker (DST). This information is typically represented as a semantic frame that captures the intent and slot-labels provided by the user. We first show that such a shallow representation is insufficient for complex dialog scenarios, because it does not capture the recursive nature inherent in many domains. We propose a recursive, hierarchical frame-based representation and show how to learn it from data. We formulate the frame generation task as a template-based tree decoding task, where the decoder recursively generates a template and then fills slot values into the template. We extend local tree-based loss functions with terms that provide global supervision and show how to optimize them end-to-end. We achieve a small improvement on the widely used ATIS dataset and a much larger improvement on a more complex dataset we describe here.",
}
```

## Dataset
This folder contains the ATIS dataset used for evaluating the proposed approach in "Recursive Template-based Frame Generation for Task Oriented Dialog"
The original ATIS dataset was modified to provide hierarchical tree representations

There are three folders: train/test/valid

Data

|

|---ATIS_modified

|--------|--train/train.tsv

|--------|--test/test.tsv

|--------|--valid/valid.tsv

|


## Data Format
All files are in TSV Format:

**Input sentence**: \t slot labels \t Hierarchical representation \t positional information

Example:
--------
Input Sentence: i want to fly from baltimore to dallas round trip .


Slot labels: O O O O O B-city_name O B-city_name B-round_trip I-round_trip O

(one slot label for every token position)


Hierarchical representation: ROOT ( atis_flight ( fromloc ( city_name ( $city_name ) ) toloc ( city_name ( $city_name ) ) round_trip ( $round_trip ) ) )


Positional information: 10 10 10 10 10 10 10 10 5 10 10 10 10 10 10 7 10 10 10 10 8 10 10 10

(Each of the labels in the hierarchical representation point to a token in the input sentence)

Non Terminals are aligned to the end of the sentence


for the above example,

ROOT points to position 10

( points to position 10

atis_flight points to position 10

( points to position 10

fromloc points to position 10

( points to position 10

city_name points to position 10

( points to position 10

$city_name points to position 5 in the input sentence (i.e., baltimore)

) points to position 10

) points to position 10

toloc points to position 10

( points to position 10

city_name points to position 10

( points to position 10

$city_name points to position 7 (i.e., dallas)

) points to position 10

) points to position 10

round_trip points to position 10

( points to position 10

$round_trip points to position 8 (i.e, round)

) points to position 10

) points to position 10

) points to position 10

## License
The data is licensed under Apache 2.0

