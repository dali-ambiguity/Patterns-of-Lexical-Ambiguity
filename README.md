# Contextualised Polyseme Word Sense Dataset v2

This is a revised and extended second version of a **Contextualised Polyseme Word Sense Dataset**. The dataset contains two human annotated measures of word sense similarity for polysemic target words used in contexts invoking different sense interpretations. The first set contains graded similarity judgements for highlighted target words displayed in two different contexts. The second set contains co-predication acceptability judgements for sentence constructions combining the sentence pairs from the first set. The paper detailing the data and our experiments will be published in Findings of EMNLP 2021. A camera-ready version is available in this repository. A first, small-scale version of the dataset was presented in [Word Sense Distance in Human Similarity Judgements and Contextualised Word Embeddings](https://www.aclweb.org/anthology/2020.pam-1.17.pdf).

This version covers the following 10 types of regular metonymic polyseme alternations:

- **animal/meat** lamb, chicken, pheasant, seagull
- **food/event** lunch, dinner
- **container-for-content** glass, bottle, cup
- **content-for-container** beer, wine, milk, juice
- **opening/physical** window, door
- **process/result** building, construction, settlement
- **physical/information** book, record
- **physical/information/organisation** newspaper, magazine
- **physical/information/medium** CD, DVD
- **building/pupils/directorate/institution** school, university

The full details on the development of the materials and the data collection can be found in the paper. In summary, we created custom samples for a set of seminal interpretations of regular metonymic polysemes and collected graded human judgements about the similarity in use across pairs of sample sentences, or the acceptability of a co-predication structure combining two context sentences.

## Materials

A full list of targets and context sentences can be found in `samples.json`. Based on these samples, we created sentence pairs and co-predication structures by combining a sentence from the *variant a* list with a sentence from the *variant b* list. If the sentence is in the same position in both lists, the resulting pairing or co-predication structure is assumed to invoke a same-sense reading, otherwise the combination elicits one of the possible cross-sense readings. The senses displayed in the *senses* list indicate the sense of each of the sentences in the two variant lists. 

The full list of target samples, including a set of test items (homonyms, synonyms, random shuffled sentences, see Appendix of the paper for more details) can be found in `similarity_samples.json` or `copredication_samples.json`, respectively. The identifiers of the samples (##\_##\_C) link to the target word (first number), the combination of senses (second number) and the order of presentation (a or b). Note that presenting a sample in inverse order technically changes the order of senses in the description. 

## Word Sense Similarity Dataset

The raw annotations of word sense similarity collected for the dataset can be found in `similarity_annotations_raw.json`, with the following structure

```
{
  "0": {
    "worker": "worker_219",
    "duration": 297,
    "annotation_run": "v2",
    "judgements": {
      "12_22_a": {
        "rating": "100"
      },
      "12_23_a": {
        "rating": "99"
      },
      ...
    },
    ...
  },
  ...
}
```

The outer key numbers individual survey submissions. Each survey contains an AMT worker's similarity judgements on 10 (v1) or 20 (v2) items. The annotation run indicates which annotation effort the data stems from (`v1` and `v1_inverse` are from the first run presented in Haber & Poesio 2020, `v2` is the extension presented in the current paper). 

Every submission has four entries: 
- `worker`, an anonymised representation of the worker's ID  
- `duration`, the duration of the submission in seconds
- `annotation_run`, indicating which annotation effort produced the data
- `judgements`, a dictionary of the submitted judgements. 

Judgements are linked to samples by their ID as indicated above. Note that because in the first annotation effort the original sample order and the inverted order were collected separately, the sample IDs do not always contain the order indicator *a* or *b*. In order to retrieve the corresponding sample for  `v1` and `v1_inverse` judgements, append *a* or *b* to the sample ID, respectively. 

Ratings range from 1 to 100.

The dataset used for our analyses excludes some items, filters out low-quality submissions and combines *a* and *b* ordering results after determining that these do not differ significantly (see the paper for details). The cleaned dataset used in the paper is saved in `similarity_judgements.json`. This dataset simply lists all target IDs and sense alternation IDs together with their collected ratings normalised to a value between 0 and 1.  

Figures visualising the word sense similarity annotations for the different combinations of sense interpretations can be found in the folder `similarty_figures`. 

## Co-predication Acceptability Dataset

The raw annotations for the co-predication acceptability can be found in `copredication_annotations_raw.json`, following the same structure as the similarity annotations. The cleaned dataset is stored in `copredication_judgements.json`. 

Figures visualising the co-predication acceptability annotations for the different combinations of sense interpretations can be found in the folder `copredication_figures`.

## Word Sense Similarity Estimates from Contextualised Language Models

Figures visualising the word sense similarity estimates for the different combinations of sense interpretations as calculated based on BERT Base, ELMo and Word2Vec can be found in the folder `computational_figures`. 

## Distributions of Annotations

The folder `distribution_figures` contains figures showing the distributions of human annotations or computational similarity ratings for same-sense vs cross-sense readings of polysemic and homonymic items in the data. The paper contains more information and a detailed analysis of these figures.

## Patterns of Lexical Ambiguity

The folder `heatmap_figures` contains figures displaying similarity maps between the different senses of a lexically ambiguous target word. There are two versions of each figure, the first one containing all senses tested in our study, the second one indicated by `_common` contains only those senses common to other targets of the same type of polysemic alternation (i.e. omits homonymic and experimental pairings). These figures can be used to investigate the patterns of sense similarity across targets allowing for the same set of sense alternations as indicated in the list above.