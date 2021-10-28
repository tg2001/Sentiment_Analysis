# Observations:

The accuracy of the model on both test and val set is more than 90%, which is good enough, but there are few important thing to notice:
- This model might not provide the correct mood of the user sometimes (or even most of the times), because a single sentence may represent several different moods,
for eg, "How could you do that?" may represent anger, sadness and surprise, depending on the context.
- This model is pretty fast that too with this accuracy, because all the stopwords are removed, which left us only with the main words to focus on and thus less number 
of columns for the model to fit.
- But for sentences like "How are you?", the end result will have no words left because each of the word in this sentence is a stopword. The model will return "joy" 
in such cases, probably because it has faced this kind of a situation and the mood in that instance was "joy". But this could actually not be the mood for sentences 
like "Why did you do that?", where the mood is probably "anger".
- This dataset has six moods: "joy", "love", "fear", "sadness", "anger", "surprise". It lacks the mood "neutral", when the user has no specific mood neither does his 
text represent any, like "I am eating" represents no specific mood. In such cases the model may output any of the above mood, which may not be correct.
- If the user enter some word that the model has never seen, then in that case the model may return inappropriate mood.
- The model treats similar words in different forms differently. Like "reply", "replies" and "replying" will be treated speareately because stemming/lemmatization is not used.
(Lemmatization took some time to run but didn't provide much improvement in accuracy, whereas stemming was fast but it instead reduced accuracy, probably because of the fact
that it changes words like "replying" to "reply" correctly but it changes "replies" to "repl" instead of "reply".)
- Tfidf Vectorizer was used instead of count vectorizer because it returns a floating point value, which is calculated based on the number of times the particular words 
appeared in the sentence and in the whole dataset. That probability is used to return the "supporting text" in the output, which gave reasonable answers in some cases.

# Possible Improvements:

- Using Deep Learning architectures like RNN or LSTM (which have a chain like structure that can refer to previous sentences/lines for getting the context) can provide 
further improvement in accuracy, at the same time providing solutions for some of the above mentioned problems.
- Online training can help in case of new words.
- Keeping stopwords and using stemming/lemmatization might also help when used with Deep Learning.
