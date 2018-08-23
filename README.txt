Permuted Dialog bAbI tasks data
-----------------------------------------------------------------------
Adaptation of the "Dialog bAbI tasks data" dataset released by Facebook, available at https://research.fb.com/downloads/babi/, under the CC BY 3.0 Unported license, available at https://creativecommons.org/licenses/by/3.0/legalcode.

This directory contains our proposed testbed for evaluating end-to-end dialog systems in the restaurant domain as described in the paper "Learning End-to-End Goal-Oriented Dialog with Multiple Answers" by Janarthanan Rajendran*, Jatin Ganhotra*, Satinder Singh and Lazaros Polymenakos (arxiv link), accepted at EMNLP 2018.
(*Equal Contribution)

Permuted-Slots-And-Restaurants
==========================================
The directory contains datasets where the slot values have been permuted and there are multiple restaurants with same rating.
The complete set of dialogs from all possible permutations of slot values and random permutation of restaurant options are in directory -
- all-permutations-dialog-bAbI-tasks/
The statistics for total number of dialogs after permutations of slots and restaurant options are mentioned in -
- all-permutations-dialog-bAbI-tasks/info.txt

From the complete set of permuted dialogs, a random subset of 1000 dialogs is taken from each of train, val, test and test-OOV sets.
These random sets of 1000 dialogs are in directory -
- permuted-dialog-bAbI-tasks/


Data format
==========================================
The file format for each task is similar to original bAbI dialog tasks, except the following changes -
ID user_utterance [tab] bot_utterance_1|{bot_utterance_2}|{bot_utterance_3}|{bot_utterance_4}
where for a given user_utterance, there can be multiple correct bot utterances, with minimum 1 bot_utterance available and maximum 4 bot_utterances.

Similar to original bAbI dialog tasks -
a) The IDs for a given  dialog start at 1 and increase. When the IDs in a file reset back to 1 you can consider the following sentences as a new dialog.
b) When the bot speaks two times in a row, we used the special token "<SILENCE>" to fill in for the missing user utterance.


For example (for task 1 utterances subset, full dialog below):
-------------------------------------------
1 hi	hello what can i help you with today
2 i'd like to book a table	i'm on it
3 <SILENCE>	where should it be|how many people would be in your party|which price range are looking for|any preference on a type of cuisine
4 madrid please	how many people would be in your party|which price range are looking for|any preference on a type of cuisine
5 for two people please	which price range are looking for|any preference on a type of cuisine
6 i am looking for a moderate restaurant	any preference on a type of cuisine
7 with italian cuisine	ok let me look into some options for you
8 <SILENCE>	api_call italian madrid two moderate

In the above example,
for turn ID=3, there are 4 possible bot_utterances -
where should it be|how many people would be in your party|which price range are looking for|any preference on a type of cuisine
for turn ID=4, there are 3 possible bot_utterances -
how many people would be in your party|which price range are looking for|any preference on a type of cuisine


For example (for task 3 utterances subset, dialog snippet below):
-------------------------------------------
28 <SILENCE>	what do you think of this option: resto_rome_expensive_french_8stars-1|what do you think of this option: resto_rome_expensive_french_8stars-2
29 do you have something else	sure let me find an other option for you
30 <SILENCE>	what do you think of this option: resto_rome_expensive_french_8stars-2
31 do you have something else	sure let me find an other option for you
32 <SILENCE>	what do you think of this option: resto_rome_expensive_french_1stars
33 that looks great	great let me do the reservation

In the above example,
for turn ID=28, there are 2 possible bot_utterances -
what do you think of this option: resto_rome_expensive_french_8stars-1|what do you think of this option: resto_rome_expensive_french_8stars-2

Similar to original bAbI dialog tasks, the goal of the tasks is to predict the bot utterances, that can be sentences or API calls (sentences starting with the special token "api_call").

For a Task 5 dialog, both of the above mentioned changes are present in a single dialog.

License
==========================================


Contact
==========================================
For more details on the dataset and baselines, see the paper "Learning End-to-End Goal-Oriented Dialog with Multiple Answers" by Janarthanan Rajendran*, Jatin Ganhotra*, Satinder Singh and Lazaros Polymenakos (arxiv link).
For any information, contact Jatin Ganhotra : jatinganhotra (at) us (dot) ibm (dot) com .
