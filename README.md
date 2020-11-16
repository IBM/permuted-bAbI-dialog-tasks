## Overview

This directory contains our proposed testbed for evaluating end-to-end dialog systems in the restaurant domain as described in the paper:  
**Learning End-to-End Goal-Oriented Dialog with Multiple Answers**  
Janarthanan Rajendran\*, Jatin Ganhotra\*, Satinder Singh and Lazaros Polymenakos [https://www.aclweb.org/anthology/Q19-1024/](https://www.aclweb.org/anthology/Q19-1024/)  
accepted at EMNLP 2018  
(**Equal Contribution*)

In a dialog, there could be multiple valid next utterances at any point. The present end-to-end neural methods for dialog do not take this into account. They learn with the assumption that at any time there is only one correct next utterance.

In this work, we focus on this problem in the goal-oriented dialog setting where there are different paths to reach a goal. We propose a new method, that uses a combination of supervised learning and reinforcement learning approaches to address this issue.

We also propose a new and more effective testbed, permuted-bAbI dialog tasks, by introducing multiple valid next utterances to the original-bAbI dialog tasks, which allows evaluation of end-to-end goal-oriented dialog systems in a more realistic setting. 

We show that there is a significant drop in performance of existing end-to-end neural methods from 81.5% per-dialog accuracy on original-bAbI dialog tasks to 30.3% on permuted-bAbI dialog tasks. We also show that our proposed method improves the performance and achieves 47.3% per-dialog accuracy on permuted-bAbI dialog tasks.


## Permuted bAbI dialog tasks

Adaptation of the "Dialog bAbI tasks data" dataset released by Facebook, available at https://research.fb.com/downloads/babi/, under the CC BY 3.0 Unported license, available at https://creativecommons.org/licenses/by/3.0/legalcode.


The directory contains datasets where the slot values have been permuted and there are multiple restaurants with same rating.

The complete set of dialogs from all possible permutations of slot values and random permutation of restaurant options are in directory - 

- all-permutations-dialog-bAbI-tasks/

The statistics for total number of dialogs after permutations of slots and restaurant options are mentioned in -

- all-permutations-dialog-bAbI-tasks/info.txt

From the complete set of permuted dialogs, a random subset of 1000 dialogs is taken from each of train, val, test and test-OOV sets. These random sets of 1000 dialogs are in directory -

- permuted-dialog-bAbI-tasks/


### Data format

The file format for each task is similar to original bAbI dialog tasks, except the following changes -
`ID user_utterance [tab] bot_utterance_1|{bot_utterance_2}|{bot_utterance_3}|{bot_utterance_4}`
where for a given user_utterance, there can be multiple correct bot utterances, with minimum 1 `bot_utterance` available and maximum 4 `bot_utterances`.

Similar to original bAbI dialog tasks -

- The IDs for a given  dialog start at 1 and increase. When the IDs in a file reset back to 1 you can consider the following sentences as a new dialog.
- When the bot speaks two times in a row, we used the special token "<SILENCE>" to fill in for the missing user utterance.


#### Example: Task 1 utterances subset:
```text
1 hi	hello what can i help you with today
2 i'd like to book a table	i'm on it
3 <SILENCE>	where should it be|how many people would be in your party|which price range are looking for|any preference on a type of cuisine
4 madrid please	how many people would be in your party|which price range are looking for|any preference on a type of cuisine
5 for two people please	which price range are looking for|any preference on a type of cuisine
6 i am looking for a moderate restaurant	any preference on a type of cuisine
7 with italian cuisine	ok let me look into some options for you
8 <SILENCE>	api_call italian madrid two moderate
```
In the above example,  
for turn ID=3, there are 4 possible bot\_utterances -
```text
where should it be|how many people would be in your party|which price range are looking for|any preference on a type of cuisine
```
for turn ID=4, there are 3 possible bot\_utterances -
```text
how many people would be in your party|which price range are looking for|any preference on a type of cuisine
```

#### Example: Task 3 utterances subset
```text
28 <SILENCE>	what do you think of this option: resto_rome_expensive_french_8stars-1|what do you think of this option: resto_rome_expensive_french_8stars-2
29 do you have something else	sure let me find an other option for you
30 <SILENCE>	what do you think of this option: resto_rome_expensive_french_8stars-2
31 do you have something else	sure let me find an other option for you
32 <SILENCE>	what do you think of this option: resto_rome_expensive_french_1stars
33 that looks great	great let me do the reservation
```
In the above example,
for turn ID=28, there are 2 possible bot_utterances -
```text
what do you think of this option: resto_rome_expensive_french_8stars-1|what do you think of this option: resto_rome_expensive_french_8stars-2
```
Similar to original bAbI dialog tasks, the goal of the tasks is to predict the bot utterances, that can be sentences or API calls (sentences starting with the special token `api_call`).

For a **Task 5 dialog**, both of the above mentioned changes are present in a single dialog.


## License

The dataset is released under [**CC BY-SA
4.0**](https://creativecommons.org/licenses/by-sa/4.0/) license. For the full
license, see [LICENSE.txt](LICENSE.txt). Please cite the following paper if you
use this dataset in your work

```text
@inproceedings{rajendran-etal-2018-learning,
    title = "Learning End-to-End Goal-Oriented Dialog with Multiple Answers",
    author = "Rajendran, Janarthanan  and
      Ganhotra, Jatin  and
      Singh, Satinder  and
      Polymenakos, Lazaros",
    booktitle = "Proceedings of the 2018 Conference on Empirical Methods in Natural Language Processing",
    month = oct # "-" # nov,
    year = "2018",
    address = "Brussels, Belgium",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/D18-1418",
    doi = "10.18653/v1/D18-1418",
    pages = "3834--3843",
    abstract = "In a dialog, there could be multiple valid next utterances at any point. The present end-to-end neural methods for dialog do not take this into account. They learn with the assumption that at any time there is only one correct next utterance. In this work, we focus on this problem in the goal-oriented dialog setting where there are different paths to reach a goal. We propose a new method, that uses a combination of supervised learning and reinforcement learning approaches to address this issue. We also propose a new and more effective testbed, permuted-bAbI dialog tasks, by introducing multiple valid next utterances to the original-bAbI dialog tasks, which allows evaluation of end-to-end goal-oriented dialog systems in a more realistic setting. We show that there is a significant drop in performance of existing end-to-end neural methods from 81.5{\%} per-dialog accuracy on original-bAbI dialog tasks to 30.3{\%} on permuted-bAbI dialog tasks. We also show that our proposed method improves the performance and achieves 47.3{\%} per-dialog accuracy on permuted-bAbI dialog tasks. We also release permuted-bAbI dialog tasks, our proposed testbed, to the community for evaluating dialog systems in a goal-oriented setting.",
}
```


## Dataset Metadata
The following table is necessary for this dataset to be indexed by search
engines such as <a href="https://g.co/datasetsearch">Google Dataset Search</a>.
<div itemscope itemtype="http://schema.org/Dataset">
<table>
  <tr>
    <th>property</th>
    <th>value</th>
  </tr>
  <tr>
    <td>name</td>
    <td><code itemprop="name">Permuted bAbI dialog task </code></td>
  </tr>
  <tr>
    <td>alternateName</td>
    <td><code itemprop="alternateName">permuted-bAbI-dialog-tasks</code></td>
  </tr>
  <tr>
    <td>url</td>
    <td><code itemprop="url">https://github.com/IBM/permuted-bAbI-dialog-tasks</code></td>
  </tr>
  <tr>
    <td>sameAs</td>
    <td><code itemprop="sameAs">https://github.com/IBM/permuted-bAbI-dialog-tasks</code></td>
  </tr>
  <tr>
    <td>description</td>
    <td><code itemprop="description">The dataset permuted-bAbI dialog tasks is an extension of original-bAbI-dialog-tasks, as described in the paper: "Learning End-to-End Goal-Oriented Dialog with Multiple Answers". We modify the original-bAbI dialog tasks, by introducing multiple valid next utterances to the original-bAbI dialog tasks, which allows evaluation of end-to-end goal-oriented dialog systems in a more realistic setting.</code></td>
  </tr>
  <tr>
    <td>provider</td>
    <td>
      <div itemscope itemtype="http://schema.org/Organization" itemprop="provider">
        <table>
          <tr>
            <th>property</th>
            <th>value</th>
          </tr>
          <tr>
            <td>name</td>
            <td><code itemprop="name">IBM</code></td>
          </tr>
          <tr>
            <td>sameAs</td>
            <td><code itemprop="sameAs">https://en.wikipedia.org/wiki/IBM</code></td>
          </tr>
        </table>
      </div>
    </td>
  </tr>
  <tr>
    <td>citation</td>
    <td><code itemprop="citation">https://www.aclweb.org/anthology/D18-1418/</code></td>
  </tr>
</table>
</div>


## Contact

For more details on the dataset and baselines, see the paper:

**Learning End-to-End Goal-Oriented Dialog with Multiple Answers**  
Janarthanan Rajendran\*, Jatin Ganhotra\*, Satinder Singh and Lazaros Polymenakos [https://www.aclweb.org/anthology/Q19-1024/](https://www.aclweb.org/anthology/Q19-1024/)  
accepted at EMNLP 2018  
(**Equal Contribution*)

For any information, contact Jatin Ganhotra : jatinganhotra (at) us (dot) ibm (dot) com .
