# HedgePeer
A Dataset for Uncertainty Detection on Peer Reviews

## Outline

- Motivation 
- Dataset : Review
- Experiments
- Acknowledgement
- Bib

## Motivation

Peer reviews are a form of scientific self-evaluation of research articles that may consist of reviews filled with uncertain information. This may be due to multiple reasons like : less proficient reviewer (in the field of publication), a polite form of writing, etc. 

Why identifying uncertainty in peer reviews important? Peer Reviews often consist the confidence level of the reviewer (manually entered by the reviewer). Many a times, a confident reviewer tends to write lackluster reviews with high degree of uncertainty. Hence, gauging the confidence of the reviewer based on their reviews is appropriate. 

Identifying uncertainty in reviews may be used as a proxy for gauging the actual confidence of the reviewer. This is where HedgePeer helps! It is the largest uncertainty detection dataset based on peer reviews.

## Dataset : Review

We introduce HedgePeer, a new dataset for uncertainty detection based on peer reviews. The Dataset can be found in the Data folder. The dataset is in the format of Jsonlines. 

### Data Format

The data is in the Jsonlines format (each line is a json object). Each line contains data corresponding to a review.

Example Entry:

```
{
    "Review_id": "B14uJzW0b_R3",
    "Sentences": [
        {
            "Sentence_id": 1,
            "Sentence": "While it is clearly written , my main concern is whether this model is significant enough .",
            "Hedges": [
                {
                    "Hedge_id": 1,
                    "Hedge": "whether",
                    "Span": "<h>  whether </h>  this model is significant enough",
                    "Hedged Sentence": "While it is clearly written, my main concern is <span>  <h>  whether </h>  this model is significant enough  </span>."
                }
            ]
        }
        ...
    ]
}
```

### Data Fields

1. Review_id : Unique id corresponding to a review file.

2. Sentence_id : Unique id for each sentence present in a review.

3. Hedge_id : Unique id corresponding to a speculative cue.

4. Hedge : Speculative word or a phrase

5. Span : It includes all constituents that fall within the uncertain interpretation corresponding to a speculative cue.

6. Hedged Sentence : A sentence with hedge and span marked. The number of hedges in a sentence would determine the number of hedged sentences for the corresponding sentence. Each hedged sentence would contain only 1 hedge and its span marked.

### Descrition of Tags for marking hedges and spans

We use special tags to enclose the hedges in a sentence. The type of tag depends on the number of words present in a speculative cue:

1. We use <h> </h> to enclose speculative words single word hedges), and

2. <mh> </mh> to enclose speculative phrases (multi word hedges)

Additionally, we enclose the spans corresponding to all hedges with <span> </span> tags.

## Experiments

We have trained several baselines on the BioScope and HedgePeer datasets. The variants used are :
- Simple Baseline
- Multi-Task Learning Baselines
  - Sentiment Intensity and POS tagging Scaffolds
  - Sentiment Intensity Scaffold and POS Late Fusion

Below are our results for Hedge cue and Span detection of several baselines on the HedgePeer dataset:

### Results on Hedge Cue Detection

| Model | Transformer | F1 Score |
| --- | --- | --- |
| Simple Baseline | SciBERT | 76.9 |
| Simple Baseline | BERT | 79.4 |
| Simple Baseline | XLNet | **84.0** |
| MTL with Sentiment | SciBERT | 72.0 |
| MTL with Sentiment | BERT | 80.6 |
| MTL with Sentiment | XLNet | 82.4 |
| MTL with Sentiment+POS | SciBERT | 72.0 |
| MTL with Sentiment+POS | BERT | 72.0 |
| MTL with Sentiment+POS | XLNet | 74.8 |
| MTL with Sentiment+POS LF | SciBERT | 71.0 |
| MTL with Sentiment+POS LF | BERT | 72.1 |
| MTL with Sentiment+POS LF | XLNet | 74.5 |

### Results on Hedge Span Detection

| Model | Transformer | F1 Score |
| --- | --- | --- |
| Simple Baseline | SciBERT | 96.6 |
| Simple Baseline | BERT | 97.0 |
| Simple Baseline | XLNet | **97.3** |
| MTL with Sentiment | SciBERT | 96.3 |
| MTL with Sentiment | BERT | 97.2 |
| MTL with Sentiment | XLNet | 97.2 |
| MTL with Sentiment+POS | SciBERT | 96.9 |
| MTL with Sentiment+POS | BERT | 97.0 |
| MTL with Sentiment+POS | XLNet | **97.3** |
| MTL with Sentiment+POS LF | SciBERT | 96.7 |
| MTL with Sentiment+POS LF | BERT | 97.0 |
| MTL with Sentiment+POS LF | XLNet | 97.1 |

## Acknowledgement

## Bib
