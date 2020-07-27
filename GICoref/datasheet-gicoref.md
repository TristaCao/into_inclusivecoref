# Gender Inclusive Coreference Dataset

By: [Yang Trista Cao](TODO:url) `<ycao95@umd.edu>` and [Hal Daumé III](http://hal3.name) `<me@hal3.name>`

As part of a study making coreference systems more gender inclusive, we collected and annotated a dataset of documents by and about non-binary and binary trans people. We call this dataset the **Gender Inclusive Coreference (GICoref) dataset**; what follows below is the [datasheet](https://arxiv.org/abs/1803.09010) describing this data. If you use this dataset, please acknowledge it by citing the original paper:

```
@inproceedings{cao2019toward,
  title={Toward Gender-Inclusive Coreference Resolution},
  author={Yang Trista Cao and Hal Daum{\'e}},
  booktitle={Proceedings of the Conference of
             the Association for Computational Linguistics (ACL)},
  year={2020},
  note={abs/1910.13913}
}
```


## Motivation


1. **For what purpose was the dataset created?** *(Was there a specific task in mind? Was there a specific gap that needed to be filled? Please provide a description.)*
    
    This dataset was created to study coreference resolution in English on documents discussing people who are, in some ways, gender-variant (and generally selected so that this variance shows up linguistically). Previously coreference resolution datasets contain nearly no such examples, largely due to the ways in which those datasets were collected (see paper for details).


1. **Who created this dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)?**
    
    This dataset was created by Yang Trista Cao and Hal Daumé III. At the time of creation, Cao was a graduate student at the University of Maryland (UMD), and Daumé is a Professor there, on leave at the time at Microsoft Research (MSR) in New York City.


1. **Who funded the creation of the dataset?** *(If there is an associated grant, please provide the name of the grantor and the grant name and number.)*
    
    Funding for Cao was provided through the UMD CS department; the annotations in the dataset were crowdsourced and funded by MSR. (The annotation was approved both by the UMD IRB and the MSR Ethics Review Board.)


1. **Any other comments?**
    
    None.





## Composition


1. **What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?** *(Are there multiple types of instances (e.g., movies, users, and ratings; people and interactions between them; nodes and edges)? Please provide a description.)*
    
    Each instance is an English document, annotated with coreference links *only for person entities*. In particular, each entity is a set of *mentions*, which are annotated as contiguous text spans. Each *mention* is assigned a numeric identifier to group them into mentions that all refer to the same entity.


2. **How many instances are there in total (of each type, if appropriate)?**
    
    The dataset consists of 95 documents from three types of sources:
     * The first are articles on English Wikipedia, in particular drawn from Wikipedia's [List of People with Non-binary Gender Identities](https://en.wikipedia.org/wiki/List_of_people_with_non-binary_gender_identities). These documents comprise about 2/3 of the dataset.
     * The second are articles from periodicals which provide coverage of LGBTQ+ issues or are aimed at the LGBTQ+ community, mostly drawn from Wikipedia's [List of LGBT Periodicals](https://en.wikipedia.org/wiki/List_of_LGBT_periodicals). These were collected by issuing a number of search queries to Google of the form `site:sss ppp`, where `sss` is the webpage for one of the periodicals, and `ppp` is a non-binary pronoun from the set {`ze+hir`, `ze+zir`, `xey+xem`, `ey+em`, `zey+zem`, `xe+xir`}. The top ten results from each site was read by one of the authors to ensure that the use of `ppp` was *actually* a use of that pronoun, and included if so. Note that because these articles were specifically returned as a result of queries for that specific set of six neo-pronoun pairs, this part of the data is unlikely to include many examples of other pronouns, and few examples of singular `they`.
     The complete set of periodicals searched were: thetransgentimes.com digitaltransgenderarchive.net ifge.org lotl.com qnews.com.au starobserver.com.au dailyxtra.com fugues.com wayves.ca thebuzzmag.ca pinkplaymags.com pink-pages.co.in attitude.co.uk mag.bent.com divamag.co.uk fyne.co.uk gaytimes.co.uk pridelife.com boyz.co.uk scotsgay.co.uk connextionsmagazine.com curvemag.com hellomrmag.com instinctmagazine.com lavendermagazine.com metrosource.com omgmag.com out.com therainbowtimesmass.com rfdmag.org pride.com travelsofadam.com plentitudemagazine.ca, though in the end we only found/included documents from The Advocate, The DailyXtra, DigitalTrans, GLReview, LambdaLiterary and Lavender. These documents comprise about 1/6 of the dataset. 
     * The third are fan-fiction stories drawn from [Archive Of Our Own](https://archiveofourown.org/) (AO3), a fan-fiction site created and run by fans, which includes a large number of stories centering around binary and non-binary trans characters. We selected stories by first considering the `Gender-Neutral Pronouns` tag (around 3700 stories), and then filtering the results to include only *General Audience* stories (vs, eg, "Mature"), to icnlude only *No Archive Warnings Apply* (vs, eg, "Graphic Descriptions of Violence" or non-consentual sex), and limited the results to "Complete Works Only." After that, we sorted the remaining approximately 900 stories by word count, and took the shortest ones that were actually stories (some were descriptions of audiobooks). These documents comprise about 1/6 of the dataset. 

    All of these sources have their own biases. Wikipedia texts tend to overuse people's deadnames, and tend to treat a person's use of pronouns as a "surprise" at the end of the document. As mentioned above, the periodical documents are specifically constrained to contain certain pronouns. And the AO3 stories are also specifically selected to have non-binary pronouns.

    Finally, to make annotation more feasible, we truncated every document at 1000 space-separated "words" prior to tokenization, so after tokenization, the documents may be somewhat longer than 1000 tokens. Finally, there were three documents which we forgot to truncate, and so made their way into the dataset at full length (these are all from AO3).

    Our annotation process was for the authors to first independently annotate the same five documents (all Wikipedia), then compare and discuss differences in annotation in an adjudication process. We then independently annotated the rest of the documents, followed by a final adjudication step. The pre-adjudication documents are also included.
    
    The overall dataset statistics below reflect this truncation:

    | Source      | #Docs | #Tokens | #Mentions | #Tok/Doc  | #Men/Doc  | #Men/Tok |
    | :---        | :---: | :---:   | :---:     | :---:     | :---:     | :---:    |
    | Wikipedia   | 63    | 42,259  | 3161      |  670      |  50       | 7.5% |
    | Periodicals | 18    | 11,210  |  753      |  622      |  41       | 6.7% |
    | AO3         | 15    | 14,881  | 2121      |  992      | 141       | 14.3% |
    | **TOTAL**   | **95** | **70,614** | **6307** | **735** | **65** | **8.9%** |

    Note here that the AO3 stories tend to be the longest in terms of number of tokens, and also are by far the most mention-dense (measured as number of mentions per token).

    **Important Note:** While annotating, we left open the possibility that an entity reference might truly be ambiguous given the context. In the end, after adjudication, one such example occurs in the data, for document `ao3_458263`. Therefore, this document appears twice in the dataset, once called `ao3_458263` and once called `ao3_458263_v2`. This is why although there are only 95 unique documents in the dataset, there are 96 annotated documents. This ambiguity is in the sentence: "She had turned the car around, amused at her own fickle impulses, and thought vaguely that what she could really do with her hair today was comb it out and have Mertle put it into those french braids *she* was so fond of." In this sentence, the first "She" refers to *Lilo*, and the final she could plausibly either refer to *Lilo* or to *Mertle* (the rest of the story does nothing to clear this up); one annotation reflects the first, the other reflects the second.


3. **Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set?** *(If the dataset is a sample, then what is the larger set? Is the sample representative of the larger set (e.g., geographic coverage)? If so, please describe how this representativeness was validated/verified. If it is not representative of the larger set, please describe why not (e.g., to cover a more diverse range of instances, because instances were withheld or unavailable).)*
    
    It is a sample of all possible documents. It is not intended to be representative (in fact, it is known to be quite non-representative): it was specifically designed to focus on documents that contains mentions of people whose gender in some way does not fall within the gender binary.


4. **What data does each instance consist of?** *(``Raw'' data (e.g., unprocessed text or images)or features? In either case, please provide a description.)*
    
    Each instance consists of text that has been sentence separated, tokenized, and annotated with mentions and entity identifiers. It is in a CoNLL-style format with bracketing for entities, as in:

    ```
    ...
    as         -
    hir        (2(3(2)
    husband    3)
    's         -
    legal      -
    spouse     2)
    ,          -
    ...
    ```
    This indicates two entities (labeled `2` and `3`). The former has two mentions, "`hir`" and "`hir husband 's legal spouse`"; the latter has one mention, "`hir husband`".
    The sentence segmentation and tokenization was initially done automatically and then (mostly) corrected by hand.
    Instances are separated in the document by lines that look like:

    `#begin document LambdaLiterary__Nearest_Exit`

    where the part before the double underscore ("`__`") is the producer, and the part after the underscore is the title of the article.


5. **Is there a label or target associated with each instance? If so, please provide a description.**
    
    The targets are the second column in the data: the mention and entity identifications.


6. **Is any information missing from individual instances?** *(If so, please provide a description, explaining why this information is missing (e.g., because it was unavailable). This does not include intentionally removed information, but might include, e.g., redacted text.)*
    
    In some cases, we removed (manually) small amounts of text from the source webpages, such as headers or footers, captions of images, and reference sections or "for further reading" sections on Wikipedia pages.


7. **Are relationships between individual instances made explicit (e.g., users' movie ratings, social network links)?** *( If so, please describe how these relationships are made explicit.)*
    
    Instances are largely unrelated, except perhaps for their source, which is mentioned in the `#begin document` section as described in the answer to question 4 in this section. Some may also be related in that they discuss the same invidividuals across different documents (e.g., [Leslie Feinberg](https://en.wikipedia.org/wiki/Leslie_Feinberg) appears at least twice in the data).


8. **Are there recommended data splits (e.g., training, development/validation, testing)?** *(If so, please provide a description of these splits, explaining the rationale behind them.)*
    
    We expect this data to be used solely for testing purposes.

    We do not explicitly provide a training/validation/testing split; however, we recognize that people may wish to do this, or to do some form of cross-validation. We would suggest cross-validation given that some phenomena only occur in a few documents, and are likely to be lost in any random split.

    **Warning:** If you *do* use any of the data for training/testing, either in a cross-validation setup or otherwise, you may wish to be careful to ensure that documents on very similar topics are always in the same split. For instance, there are two documents about Leslie Feinberg in the dataset; you should ensure that these are in the same split or evaluation scores are likely to be inflated.


9. **Are there any errors, sources of noise, or redundancies in the dataset?** *(If so, please provide a description.)*
    
    There are almost certainly some errors in tokenization, and annotation. We did our best to minimize these, but some certainly remain. As mentioned in the previous question, there are some documents about the same people (though from different sources).


10. **Is the dataset self-contained, or does it link to or otherwise rely on external resources (e.g., websites, tweets, other datasets)?** *(If it links to or relies on external resources, a) are there guarantees that they will exist, and remain constant, over time; b) are there official archival versions of the complete dataset (i.e., including the external resources as they existed at the time the dataset was created); c) are there any restrictions (e.g., licenses, fees) associated with any of the external resources that might apply to a future user? Please provide descriptions of all external resources and any restrictions associated with them, as well as links or other access points, as appropriate.)*
    
    The dataset is self-contained.


11. **Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by doctor-patient confidentiality, data that includes the content of individuals' non-public communications)?** *(If so, please provide a description.)*
    
    No; all raw data in the dataset is from public sources (Wikipedia, online periodicals, or online open fan-fiction).


12. **Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?** *(If so, please describe why.)*
    
    All documents deal with people, some of whom have had traumatic events in their lives that are discussed, particularly around their gender identities. All should be read with that in mind. Some of the articles, especially from fan-fiction, have explicit and intentional misgendering of characters, and a few describe (or hint out) intimate relationships (though we filtered for only stories that did not have "adult themes").


13. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*
    
    Yes, most of the articles relate to real people (except the fan-fiction articles).


14. **Does the dataset identify any subpopulations (e.g., by age, gender)?** *(If so, please describe how these subpopulations are identified and provide a description of their respective distributions within the dataset.)*
    
    This is not explicitly identified, though many of the articles explicitly mention the gender of the people described/discussed.


15. **Is it possible to identify individuals (i.e., one or more natural persons), either directly or indirectly (i.e., in combination with other data) from the dataset?** *(If so, please describe how.)*
    
    Yes; their names are given in running text.


16. **Does the dataset contain data that might be considered sensitive in any way (e.g., data that reveals racial or ethnic origins, sexual orientations, religious beliefs, political opinions or union memberships, or locations; financial or health data; biometric or genetic data; forms of government identification, such as social security numbers; criminal history)?** *(If so, please provide a description.)*
    
    The gender information given may be sensitive in certain situations, at least for those articles dealing with real people. However, all these articles are from either Wikipedia or periodicles, and is therefore already public information.


17. **Any other comments?**
    
    None.





## Collection Process


1. **How was the data associated with each instance acquired?** *(Was the data directly observable (e.g., raw text, movie ratings), reported by subjects (e.g., survey responses), or indirectly inferred/derived from other data (e.g., part-of-speech tags, model-based guesses for age or language)? If data was reported by subjects or indirectly inferred/derived from other data, was the data validated/verified? If so, please describe how.)*
    
    The data was all downloaded directly from associated webpages (Wikipedia, periodicals, or AO3). Tokenization and sentence segmentation was initially done automatically but corrected by hand.


1. **What mechanisms or procedures were used to collect the data (e.g., hardware apparatus or sensor, manual human curation, software program, software API)?** *(How were these mechanisms or procedures validated?)*
    
    Annotation was conducted using [TagEditor](https://github.com/d5555/TagEditor).


1. **If the dataset is a sample from a larger set, what was the sampling strategy (e.g., deterministic, probabilistic with specific sampling probabilities)?**
    
    See answer to question #2 in [Composition](#composition).


1. **Who was involved in the data collection process (e.g., students, crowdworkers, contractors) and how were they compensated (e.g., how much were crowdworkers paid)?**
    
    All collection and annotation was done by the two authors.


1. **Over what timeframe was the data collected?** *(Does this timeframe match the creation timeframe of the data associated with the instances (e.g., recent crawl of old news articles)?  If not, please describe the timeframe in which the data associated with the instances was created.)*
    
    The dataset was collected in the early Summer of 2019, which does not necessarily reflect the timeframe of the data collected.


1. **Were any ethical review processes conducted (e.g., by an institutional review board)?** *(If so, please provide a description of these review processes, including the outcomes, as well as a link or other access point to any supporting documentation.)*
    
    No review processes were conducted with respect to the collection and annotation of this data (though review was done for other aspects of this work; see the paper linked at the top of the datasheet).


1. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*
    
    Yes; the majority of the documents in the dataset are articles about people (either their Wikipedia entries or stories about them in periodicals).


1. **Did you collect the data from the individuals in question directly, or obtain it via third parties or other sources (e.g., websites)?**
    
    Other sources: Wikipedia and periodicals.


1. **Were the individuals in question notified about the data collection?** *(If so, please describe (or show with screenshots or other information) how notice was provided, and provide a link or other access point to, or otherwise reproduce, the exact language of the notification itself.)*
    
    No, they were not notified.


1. **Did the individuals in question consent to the collection and use of their data?** *(If so, please describe (or show with screenshots or other information) how consent was requested and provided, and provide a link or other access point to, or otherwise reproduce, the exact language to which the individuals consented.)*
    
    No. All documents are public. In the case of the AO3 stories, we explicitly contacted the authors and received permission to use their stories. (Several authors we contacted did not respond; we did not include their stories.)


1. **If consent was obtained, were the consenting individuals provided with a mechanism to revoke their consent in the future or for certain uses?** *(If so, please provide a description, as well as a link or other access point to the mechanism (if appropriate).)*
    
    N/A.


1. **Has an analysis of the potential impact of the dataset and its use on data subjects (e.g., a data protection impact analysis) been conducted?** *(If so, please provide a description of this analysis, including the outcomes, as well as a link or other access point to any supporting documentation.)*
    
    No. 


1. **Any other comments?**
    
    None.





## Preprocessing/cleaning/labeling


1. **Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)?** *(If so, please provide a description. If not, you may skip the remainder of the questions in this section.)*
    
    Yes; the documents were truncated at 1000 words, sentence split and tokenized.


1. **Was the "raw" data saved in addition to the preprocessed/cleaned/labeled data (e.g., to support unanticipated future uses)?** *(If so, please provide a link or other access point to the "raw" data.)*
    
    Yes, the original raw data is included in the distribution, in the folder `raw`.


1. **Is the software used to preprocess/clean/label the instances available?** *(If so, please provide a link or other access point.)*
    
    Yes; it is [TagEditor](https://github.com/d5555/TagEditor) version 1.5.


1. **Any other comments?**
    
    None.





## Uses


1. **Has the dataset been used for any tasks already?** *(If so, please provide a description.)*
    
    The dataset has been used to understand human annotation biases and to test existing coreference systems. See the paper linked at the top for more details.


1. **Is there a repository that links to any or all papers or systems that use the dataset?** *(If so, please provide a link or other access point.)*
    
    No.


1. **What (other) tasks could the dataset be used for?**
    
    The dataset could possibly be used for developing or testing systems for referring expression generation. 


1. **Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?** *(For example, is there anything that a future user might need to know to avoid uses that could result in unfair treatment of individuals or groups (e.g., stereotyping, quality of service issues) or other undesirable harms (e.g., financial harms, legal risks)  If so, please provide a description. Is there anything a future user could do to mitigate these undesirable harms?)*
    
    While the dataset was specifically constructed to be gender inclusive, it undoubtedly fails in some ways to full achieve that goal. Part of this is due to the nature of the underlying texts (eg, Wikipedia's frequent use of deadnames) and part of it is due to plain difficulties in collection (automatically distinguishing specific singular uses of "they" from other uses is currently not possible, and so despite "they" being currently, likely, the most commonly used non-binary pronoun, it is perhaps underrepresented in this dataset). Preprocessing hopefully did not introduce errors (in fact, we corrected for many tokenization errors, for instance, that the default tokenizer did not know to split "xe'll" into two tokens as it would "she'll").


1. **Are there tasks for which the dataset should not be used?** *(If so, please provide a description.)*
    
    This dataset should not be used for any sort of "gender prediction." First, anyone using this dataset (or any related dataset, for that matter), should recognize that "gender" doesn't mean any single thing, and furthermore that pronoun != gender. Furthermore, because of the fluid and temporal notion of gender--and of gendered referring expressions like pronouns and terms of address--just because a person is described in this dataset in one particular way, does not mean that this will always be the appropriate way to refer to this person.


2. **Any other comments?**
    
    None.




## Distribution


1. **Will the dataset be distributed to third parties outside of the entity (e.g., company, institution, organization) on behalf of which the dataset was created?** *(If so, please provide a description.)*
    
    Yes, the dataset is freely available.


1. **How will the dataset will be distributed (e.g., tarball  on website, API, GitHub)?** *(Does the dataset have a digital object identifier (DOI)?)*
    
    The dataset is free for download at github.com/hal3/gicoref-dataset.


1. **When will the dataset be distributed?**
    
    The dataset is distributed as of June 2020 in its first version.


1. **Will the dataset be distributed under a copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?** *(If so, please describe this license and/or ToU, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms or ToU, as well as any fees associated with these restrictions.)*
    
    The dataset is licensed under a BSD license.


1. **Have any third parties imposed IP-based or other restrictions on the data associated with the instances?** *(If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms, as well as any fees associated with these restrictions.)*
    
    Not to our knowledge.


1. **Do any export controls or other regulatory restrictions apply to the dataset or to individual instances?** *(If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any supporting documentation.)*
    
    Not to our knowledge.


1. **Any other comments?**
    
    None.





## Maintenance


1. **Who is supporting/hosting/maintaining the dataset?**
    
    Both authors (Trista Cao and Hal Daumé III) are maintaining. Hal is hosting on github.


1. **How can the owner/curator/manager of the dataset be contacted (e.g., email address)?**
    
    E-mail addresses are at the top of this document.


1. **Is there an erratum?** *(If so, please provide a link or other access point.)*
    
    Currently, no. As errors are encountered, future versions of the dataset may be released (but will be versioned). They will all be provided in the same github location.


1. **Will the dataset be updated (e.g., to correct labeling errors, add new instances, delete instances')?** *(If so, please describe how often, by whom, and how updates will be communicated to users (e.g., mailing list, GitHub)?)*
    
    Same as previous.


1. **If the dataset relates to people, are there applicable limits on the retention of the data associated with the instances (e.g., were individuals in question told that their data would be retained for a fixed period of time and then deleted)?** *(If so, please describe these limits and explain how they will be enforced.)*
    
    No.


1. **Will older versions of the dataset continue to be supported/hosted/maintained?** *(If so, please describe how. If not, please describe how its obsolescence will be communicated to users.)*
    
    Yes; all data will be versioned.


1. **If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for them to do so?** *(If so, please provide a description. Will these contributions be validated/verified? If so, please describe how. If not, why not? Is there a process for communicating/distributing these contributions to other users? If so, please provide a description.)*
    
    Errors may be submitted via the bugtracker on github. More extensive augmentations may be accepted at the authors' discretion.


1. **Any other comments?**
    
    None.


