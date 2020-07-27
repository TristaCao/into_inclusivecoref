# Maybe Ambiguous Pronoun Dataset - MAP

By: [Yang Trista Cao](http://ycao95.umiacs.io/) `<ycao95@umd.edu>` and [Hal Daumé III](http://hal3.name) `<me@hal3.name>`

As part of a study making coreference systems more gender inclusive, we studied how gender bias can exist in data collection through human annotations. In order to determine which gender cues annotators are using and the degree to which they use them, we construct an ablation study in which we hide various aspects of gender and evaluate how this impacts annotators’ judgments of anaphoricity. We call this dataset the **Maybe Ambiguous Pronoun (MAP) dataset**; what follows below is the [datasheet](https://arxiv.org/abs/1803.09010) describing this data. If you use this dataset, please acknowledge it by citing the original paper:

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
    
    This dataset was created to study gender bias in coreference resolution data annotation. Arising from a combination of (possibly) underspecied annotations guidelines and the positionality of annotators themselves.

1. **Who created this dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)?**
    
    This dataset was created by Trista Cao and Hal Daumé III. At the time of creation, Cao was a graduate student at the University of Maryland (UMD), and Daumé was a Professor there, on leave at the time at Microsoft Research (MSR) in New York City.


1. **Who funded the creation of the dataset?** *(If there is an associated grant, please provide the name of the grantor and the grant name and number.)*
    
    Funding for Cao was provided through the UMD CS department; the annotations in the dataset were crowdsourced and funded by MSR. (The annotation was approved both by the UMD IRB and the MSR Ethics Review Board.)


1. **Any other comments?**
    
    None





## Composition


1. **What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?** *(Are there multiple types of instances (e.g., movies, users, and ratings; people and interactions between them; nodes and edges)? Please provide a description.)*
    
    Each instance is an English text snippet (1-2 sentences), which includes at least two person-entities referenced by name and one third-person singular pronoun (here we only consider binary pronouns) that refers to one of the two person-entities. With the snippet, each instance also includes the correct coreference and human-annotated coreference of the pronoun with the person-entity.


1. **How many instances are there in total (of each type, if appropriate)?**
    
    The dataset consists of 549 instances, whose text snippets are naturally occurring texts extracted from English Wikipedia articles, and 4941 instances, whose text snippets were automatically modified from the 549 natural snippets following the nine forms of ablation (9 forms of ablation * 549 natural snippets = 4941 instances). See the paper linked at the top for details of the nine forms of ablation of gender cues. Thus, in total, there are 549 + 4941 = 1830 instances in the dataset. 


1. **Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set?** *(If the dataset is a sample, then what is the larger set? Is the sample representative of the larger set (e.g., geographic coverage)? If so, please describe how this representativeness was validated/verified. If it is not representative of the larger set, please describe why not (e.g., to cover a more diverse range of instances, because instances were withheld or unavailable).]* 
    
    The dataset is a sample of text snippets from all Wikipedia articles. It is not representative, since we intentionally want a balanced dataset of masculine and feminine referents, while Wikipedia articles have way more masculine referents than feminine ones. 


1. **What data does each instance consist of?** *(''Raw'' data (e.g., unprocessed text or images)or features? In either case, please provide a description.)*
    
    Each instance consists of 12 features. 
    1. id -- The identity of the instance, which consists of the identity of the original text + the ablated form applied. E.g. 
            "new-106+addr+pro" indicates that the "full-text" of this instance is the text of "new-106" with terms of address and pronoun gender cues ablated.
    2. full-text -- The text snippet with at least two person-entities referenced by name and one third-person singular pronoun. The 
    				text snippet is either naturally occurring (original) text from Wikipedia articles or modified text using one of the nine ablation forms.
	3. A -- The name of the first person-entity in the "full-text."
	4. A-offset -- The character-wise position of "A" in the "full-text."
	5. B -- The name of the second person-entity in the "full-text."
	6. B-offset -- The character-wise position of "B" in the "full-text."
	7. Pronoun -- The third-person singular pronoun in the "full-text."
    8. Pronoun-offset -- The character-wise position of "Pronoun" in the "full-text."
    9. Answer -- The ground-truth of the coreference. 
               (0 -> pronoun refers to A; 
                1 -> pronoun could refer to either A or B; 
                2 -> pronoun refers to B; 
                3 -> pronoun refers to neither A nor B)
    10. Human1 -- First human annotaiton result of the coreference.
               (0 -> pronoun very likely refers to A; 
                1 -> pronoun probably refers to A;
                2 -> pronoun could refer to either A or B;
                3 -> pronoun probably refers to B;
                4 -> pronoun very likely refers to B;
                5 -> pronoun refers to neither A nor B)
    11. Human2 -- Second human annotation result of the coreference.
    12. Human3 -- Third human annotation result of the coreference.


1. **Is there a label or target associated with each instance? If so, please provide a description.**
    
    The label is the "Answer", "Human1", "Human2", and "Human3" features: the correct and human-annotated coreference results. 


1. **Is any information missing from individual instances?** *(If so, please provide a description, explaining why this information is missing (e.g., because it was unavailable). This does not include intentionally removed information, but might include, e.g., redacted text.)*
    
    Some instances do not have all three human annotation results ("Human1", "Human2", and "Human3"). This is because we removed annotations that did not pass our tests (see question #1 in [Collection Process](#collectionprocess)).


1. **Are relationships between individual instances made explicit (e.g., users' movie ratings, social network links)?** *( If so, please describe how these relationships are made explicit.)*
    
    Instances are largely unrelated. Text snippet were extracted all from different Wikipedia articles.  


1. **Are there recommended data splits (e.g., training, development/validation, testing)?** *(If so, please provide a description of these splits, explaining the rationale behind them.)*
    
    No.  


1. **Are there any errors, sources of noise, or redundancies in the dataset?** *(If so, please provide a description.)*
    
    There are almost certainly some noise in annotation. We collected annotations using Amazon Mechanical Turk. Though we tried to reduce annotation noise by inserting test questions, the result annotation certainly remain some noise. 


1. **Is the dataset self-contained, or does it link to or otherwise rely on external resources (e.g., websites, tweets, other datasets)?** *(If it links to or relies on external resources, a) are there guarantees that they will exist, and remain constant, over time; b) are there official archival versions of the complete dataset (i.e., including the external resources as they existed at the time the dataset was created); c) are there any restrictions (e.g., licenses, fees) associated with any of the external resources that might apply to a future user? Please provide descriptions of all external resources and any restrictions associated with them, as well as links or other access points, as appropriate.)*
    
    The dataset is self-contained.


1. **Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by doctor-patient confidentiality, data that includes the content of individuals' non-public communications)?** *(If so, please provide a description.)*
    
    No; all raw data in the dataset is from public Wikipedia.


1. **Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?** *(If so, please describe why.)*
    
    No.


1. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*
    
    Yes, each instance includes at least two person entities (most of them are real-person entities). Also the text snippets are most likely from the Wikipedia article about one of these two person entities.


1. **Does the dataset identify any subpopulations (e.g., by age, gender)?** *(If so, please describe how these subpopulations are identified and provide a description of their respective distributions within the dataset.)*
    
    No. 


1. **Is it possible to identify individuals (i.e., one or more natural persons), either directly or indirectly (i.e., in combination with other data) from the dataset?** *(If so, please describe how.)*
    
    Yes; their names are given in the text snippets.


1. **Does the dataset contain data that might be considered sensitive in any way (e.g., data that reveals racial or ethnic origins, sexual orientations, religious beliefs, political opinions or union memberships, or locations; financial or health data; biometric or genetic data; forms of government identification, such as social security numbers; criminal history)?** *(If so, please provide a description.)*
    
    This is not explicitly identified, though some text snippets can be from Wikipedia articles that contain sensitive information. However, all these text snippets are from Wikipedia, and is therefore already public information.


1. **Any other comments?**
    
    No.





## Collection Process


1. **How was the data associated with each instance acquired?** *(Was the data directly observable (e.g., raw text, movie ratings), reported by subjects (e.g., survey responses), or indirectly inferred/derived from other data (e.g., part-of-speech tags, model-based guesses for age or language)? If data was reported by subjects or indirectly inferred/derived from other data, was the data validated/verified? If so, please describe how.)*
    
    p1: crawl from wiki -- NER, pronoun list
    p2: offset -- 
    p3: ablation -- sem list
    p4: annotation -- guidline, choices, test cases
    The data collection process involves four parts.

    Part1 - Text Snippets Collection:
    		All text snippets are from Wikipedia articles that were randomly selected. Then for each article, we passed through each sentences to check if it contains two name entities and one pronoun (here we only focus on binary third-person singular pronoun). If so we collect this sentence with its previous sentence and skip to the next article. In addition, we intentionally picked the same number of text snippets with feminine pronouns as snippets with masculine pronouns. 
    
    Part2 - Features Extraction and Annotation:
    		Given the text snippet (feature 'full-text') with two name entities (features 'A' and 'B') and the pronoun, we ran some scripts to count the character-wise position of the name entities and the pronoun (feature offsets). Then we ask crowdworkers from MTurk to annotate which of the two names the pronoun refers to. For each text snippet, we assign three crowdworkers. Crowdworkers were paid $1 to annotate 10 text snippets. We use majority vote as the ground-truth (feature 'answer'). For instances that did not have a majority, we hand annotated them. 
    
    Part3 - Ablation of Gender Cues:
    		There are four kinds of gender cues we consider: pronouns, names, terms of address, and semantically gendered nouns. See the paper linked at the top for explainations of those gender cues. We ran scripts to automatically ablate those gender cues in the text snippets and modify corresponding features for each instance. 
    		
    		For pronouns substitution, all binary third-person singular pronouns were replaced with non-binary pronouns (see list below). Different forms of the same pronoun were mapped to the same group of non-binary pronouns (e.g. He likes his new book. -> Ze likes hir new book). We also generate dependency parses to distinguish 'his' in "his frusbee" and "it was his", and 'her' in "her frisbee" and "went with her".
    		```
    		he/she          -> they/ze/ey/xey
    		him/her         -> them/hir/em/xem
    		his/her         -> their/hir/eir/xyr
    		his/hers        -> theirs/hirs/eirs/xyrs
    		himself/herself -> themself/hirself/eirself/xemself
    		```

    		For names substituion, we repalce all names (e.g., “Aditya Modi”) by a random name with only a first initial and a last name (e.g., “B. Hernandez”). We did our best to make sure different forms of the same name were mapped to the same random name (e.g. "Aditya Modi" and "Aditya" -> "B. Hernandez", "Mr. Modi" -> "Mr. Hernandez"). 

    		For terms of address, we remove all of them. Below is the list of terms of address we considered. 
    		```
    		Mr, Mrs, Mister, Miss, Ms, Mme, Mlle, Sir, Madame, Ma'am, Dame, Esq, Adv, Gentleman, Sire, Excellence, Excellency, Abbot
    		```

    		For semantically gendered nouns, we replace all semantically gendered nouns with a gender-indefinite variant. The list of those nouns and corresponding variants are attached as "sem.csv". This list was collected from the following websites and manually modified by the authors.
    		```
    		https://www.iluenglish.com/gender-in-english-masculine-and-feminine-words/
			https://www.myenglishpages.com/site_php_files/grammar-lesson-masculine-feminine.php
			https://7esl.com/gender-of-nouns/
			http://myenglishgrammar.com/list-20-gender.html
			https://educationwithfun.com/course/view.php?id=27&section=7
			https://englishgrammarrulestenses.blogspot.com/2014/01/masculine-and-feminine-words-list-in_18.html
			http://engengenglish.blogspot.com/2009/11/list-of-genders.html
			```

	Part4 - Human Annotation:
			Fianlly we collected crowdworker annotations on the original text snippets and their 9 forms of ablations. Each annotation page thus consists of 10 questions plus 1 random test question from the [GAP](https://github.com/google-research-datasets/gap-coreference) dataset. When the test fails, all annotations from this page were removed. We used Amazon Machanical Turk to collect annotations. Crowdworkers were paid $1 to annotate 11 instances. For each instance, we collect 3 annotations.

    

1. **What mechanisms or procedures were used to collect the data (e.g., hardware apparatus or sensor, manual human curation, software program, software API)?** *(How were these mechanisms or procedures validated?)*
    
    In part1 of the data collection process, we use [AllenNLP Name Entity Recognition model](https://demo.allennlp.org/named-entity-recognition) to detect name entities in sentences.


1. **If the dataset is a sample from a larger set, what was the sampling strategy (e.g., deterministic, probabilistic with specific sampling probabilities)?**
    
    The text snippets were selected randomly from all English Wikipedia articles.


1. **Who was involved in the data collection process (e.g., students, crowdworkers, contractors) and how were they compensated (e.g., how much were crowdworkers paid)?**
    
    Data collection was done by the two authors and data annotation was done by crowdworkers form Amazon Mechanical Turk. 


1. **Over what timeframe was the data collected?** *( Does this timeframe match the creation timeframe of the data associated with the instances (e.g., recent crawl of old news articles)?  If not, please describe the timeframe in which the data associated with the instances was created.)*
    
    The dataset was collected in the early Summer of 2019.


1. **Were any ethical review processes conducted (e.g., by an institutional review board)?** *(If so, please provide a description of these review processes, including the outcomes, as well as a link or other access point to any supporting documentation.)*
    
    No review processes were conducted with respect to the collection and annotation of this data (though review was done for other aspects of this work; see the paper linked at the top of the datasheet).


1. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*
    
    Yes; the majority of the text snippets are extracted from Wikipedia articles about people.


1. **Did you collect the data from the individuals in question directly, or obtain it via third parties or other sources (e.g., websites)?**
    
    Other sources: Wikipedia.


1. **Were the individuals in question notified about the data collection?** *(If so, please describe (or show with screenshots or other information) how notice was provided, and provide a link or other access point to, or otherwise reproduce, the exact language of the notification itself.)*
    
    No, they were not notified.


1. **Did the individuals in question consent to the collection and use of their data?** *(If so, please describe (or show with screenshots or other information) how consent was requested and provided, and provide a link or other access point to, or otherwise reproduce, the exact language to which the individuals consented.)*
    
    No. All articles are from Wikipedia and thus are public.


1. **If consent was obtained, were the consenting individuals provided with a mechanism to revoke their consent in the future or for certain uses?** *(If so, please provide a description, as well as a link or other access point to the mechanism (if appropriate).)*
    
    N/A.


1. **Has an analysis of the potential impact of the dataset and its use on data subjects (e.g., a data protection impact analysis)been conducted?** *(If so, please provide a description of this analysis, including the outcomes, as well as a link or other access point to any supporting documentation.)*
    
    No.


1. **Any other comments?**
    
    None.





## Preprocessing/cleaning/labeling


1. **Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)?** *(If so, please provide a description. If not, you may skip the remainder of the questions in this section.)*
    
    See answer to question #1 in [Collection Process](#collectionprocess)


1. **Was the "raw" data saved in addition to the preprocessed/cleaned/labeled data (e.g., to support unanticipated future uses)?** *(If so, please provide a link or other access point to the "raw" data.)*
    
    No.


1. **Is the software used to preprocess/clean/label the instances available?** *(If so, please provide a link or other access point.)*
    
    See answer to question #2 in [Collection Process](#collectionprocess)


1. **Any other comments?**
    
    None.





## Uses


1. **Has the dataset been used for any tasks already?** *(If so, please provide a description.)*
    
    The dataset has been used to understand human annotation biases and to test existing coreference systems. See the paper linked at the top for more details.


1. **Is there a repository that links to any or all papers or systems that use the dataset?** *(If so, please provide a link or other access point.)*
    
    No.


1. **What (other) tasks could the dataset be used for?**
    
    The dataset could possibly be used for analyzing how human handle coreference resolution tasks. 


1. **Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?** *(For example, is there anything that a future user might need to know to avoid uses that could result in unfair treatment of individuals or groups (e.g., stereotyping, quality of service issues) or other undesirable harms (e.g., financial harms, legal risks)  If so, please provide a description. Is there anything a future user could do to mitigate these undesirable harms?)*
    
    Since the ablations were done automatically, those modified text snippets can be quite aritificial.


1. **Are there tasks for which the dataset should not be used?** *(If so, please provide a description.)*
    
    This dataset should not be used for any sort of "gender prediction." First, anyone using this dataset (or any related dataset, for that matter), should recognize that "gender" doesn't mean any single thing, and furthermore that pronoun != gender. Furthermore, because of the fluid and temporal notion of gender--and of gendered referring expressions like pronouns and terms of address--just because a person is described in this dataset in one particular way, does not mean that this will always be the appropriate way to refer to this person.



1. **Any other comments?**
    
    None.




## Distribution


1. **Will the dataset be distributed to third parties outside of the entity (e.g., company, institution, organization) on behalf of which the dataset was created?** *(If so, please provide a description.)*
    
    Yes, the dataset is freely available.


1. **How will the dataset will be distributed (e.g., tarball  on website, API, GitHub)?** *(Does the dataset have a digital object identifier (DOI)?)*
    
    The dataset is free for download at https://github.com/TristaCao/into_inclusivecoref.


1. **When will the dataset be distributed?**
    
    The dataset is distributed as of July 2020 in its first version.


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
    
    Both authors (Yang Trista Cao and Hal Daumé III) are maintaining. Trista is hosting on github.


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


