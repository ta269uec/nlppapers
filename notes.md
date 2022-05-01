# Notes on paper ideas

## [Is preprocessing of text really worth your time for toxic comment classification?](https://arxiv.org/pdf/1806.02908.pdf)

### Abstract
Authors study impact of text transformation for toxic comment datasets (Jigsaw) and conclude no  transformation produce relatively decent model and basic transformations, in some cases, lead to worse performance.

Online comments data has non-standard English words full of typos and spurious characters. Multi-folds including originating from mobile devices, use of acronyms, leetspeak words (http://1337.me/), or intentionally obfuscating words (abusive) to avoid filters by inserting spurious characters, using phonemes, dropping characters etc. leading to feature explosion and difficulty training model.

### Related Work

1. Bao et. al. used five transformations namely URLs features reservation, negation transformation, repeated letters normalization, stemming and lemmatization on twitter data and applied linear classifier and found the accuracy of the classification increases when URLs features reservation, negation transformation and repeated letters normalization are employed while decreases when stemming and lemmatization are applied [19].

2. Jianqiang and Xiaolin found removal of URLs, the removal of stop words and the removal of numbers have minimal effect on accuracy whereas replacing negation and expanding acronyms can improve the accuracy.

3. Most of the authors used conventional ML models such as SVM, LR, RF and NB. We are expanding our candidate pool for transformations and using latest state-of-the-art models such as LR, NBSVM, XGBoost and Bidirectional LSTM model using fastTextâA˘ Zs skipgram ´ word vector.

### Contributions
In this paper we have identified 20 different atomic transformations (plus 15 sequence of transformations) to preprocess the texts.

1. Remove rare words: In the Jigsaw toxic text corpora, a staggering 65.3% of the words occurred just once and 88.3% of the words appeared five or less number of times (See Fig. 2(a)). This shows that there are many different ways to represent the same words. The Fig. 2(b) below shows different number of ways (that we could identify, actual number may be more) some of the abusive words are written in the Jigsaw corpora.

2. Use regular expression for blacklisted words: A regular expression is created for each one of the blacklisted word and every word in corpora is compared to see which is matched. The âAŸ*â ˘ A˘ Z (asterisk) is assumed ´ to be the wild character that can match any character. Our algorithm knows that s**t, S***T, sh**, shi*, s*it:), SHYT, sHYt, shiiiit, shiiiiiiiiiiiit and siht, all represent the same word.

3. Check if the words if they look like proper name: A large number of words with frequency less than 10 looked like proper names (person, city or other proper names). We matched each words with compiled list of 1) city names 2) countries 3) nationalities 4) ethnicities 5) names of persons (a. English names, b. Spanish names, c. Hindi first names, d. Hindi last names e. Muslim names). • Replace profane words using fuzzy matching: We used fuzzy matching to see how close a word is to the abusive words based on Levenshtein distance. By carefully selecting the threshold based on empirical value, the algorithm can detect that the words; SHUIT, SHYT, SHIZZ, SHiiT, SHITV, $h1+, $hit, 5h1t; represent the same word.

4. Replace common words using fuzzy matching. In this transformation, we assumed that any word with a frequency of more than 100 (empirically chosen) is frequent word. Then we normalized these frequent words by removing all non-alphanumeric characters and resulted in 4,606 unique frequent words. Then, we fuzzy matched all the raw words in corpora with frequent word to get the closest word. A matching percent threshold matching_pct is used to decide if a word is a match with a frequent word )

### Conclusions

Time spent on preprocessing and various combinations didn't help, rather impacted performance. Authors are unclear about the reason and suspect toxic data is long unlike twitter which is character limited

# [The Role of Pre-processing in Twitter Sentiment Analysis](https://www.researchgate.net/publication/339982951_The_Role_of_Pre-processing_in_Twitter_Sentiment_Analysis)

## Synopsis

1. We evaluate the effects of URLs, negation, repeated letters, stemming and lemmatization. 
Experimental results on the Stanford Twitter Sentiment Dataset show that sentiment classification accuracy 
rises when URLs features reservation, negation transformation and repeated letters normalization are employed 
while descends when stemming and lemmatization are applied. 
Moreover, we get a better result by augmenting the original feature space with bigram and emotions features. 
Comprehensive application of these measures makes us achieve classification accuracy of 85.5%.

2. The above works are focused on products reviews, which are always
well-organized sentences and relate to a particular domain. In contrast, tweets, whose
length is limitted to 140 characters, are casual in the language style and multifarious
in fields and themes. Moreover tweets contain a large amount of noises, such as
hashtags, URLs, and emotions. These characters make Twitter sentiment analysis a
challenging assignment

# [POLYLOSS: A POLYNOMIAL EXPANSION PERSPECTIVE OF CLASSIFICATION LOSS FUNCTIONS](https://arxiv.org/pdf/2204.12511.pdf)

## Synopsis

Cross-entropy loss and focal loss are the most common choices when training
deep neural networks for classification problems. Generally speaking, however, a
good loss function can take on much more flexible forms, and should be tailored
for different tasks and datasets. Motivated by how functions can be approximated
via Taylor expansion, we propose a simple framework, named PolyLoss, to view
and design loss functions as a linear combination of polynomial functions. Our
PolyLoss allows the importance of different polynomial bases to be easily adjusted depending on the targeting tasks and datasets, while naturally subsuming
the aforementioned cross-entropy loss and focal loss as special cases
