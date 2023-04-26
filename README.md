# Stack Overflow Daml app

Daml templates for a platform that allows users to ask questions and get answers, similar to Stack Overflow.

## Overview

One user may ask questions, and any number of other users may propose answers to this question. Finally, the party who asked the question may accept one of the answers as the approved answer.

All questions and answers are publicly viewable.

## Example flow

1. Bob asks a question
2. Alice proposes an answer to Bob's question
3. Charlie also proposes and answer to Bob's question
4. Bob accepts Charlie's answer to his question

## Challenges

* Since the intention is to mimic Stack Overflow, where all questions and answers are publicly viewable, both the Question and Answer contract must be viewable by everyone. Therefore both these contracts include a Party named `public`, with the intent that everyone can act as this party in order to browse questions and answers.

* Since the act of accepting an aswer will archive an existing Question (that has no answer) and create a new one with the `answer` field set, answers must not refer to a question by its ContractId. If it did, then the act of accepting an answer to a question would make all answers to a question point to an archived contract. Instead, a key is used to refer to a Question. This key has two components: the Party who asked the question (the *asker*) as well as an integer ID (which must be unique for each *asker*). Consequently, when *partyA* creates a new Question, it's necessary to look up the latest integer ID for *partyA* and create the new question with this field incremented by one.

## Instructions

### Building
To compile the project run:
```
daml build
```

### Testing
To test the project run:
```
daml test
```

### Running
To load the project into the sandbox and start navigator run:
```
daml start
```
