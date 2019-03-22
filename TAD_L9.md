# Text-As-Data
### Lecture 9 - Classification (2)
---

### Overfitting

Overfitting is a **modelling error** that occurs when a function is too closely fit to a limited set of data points.

The data in reality has some degree of **error or random noise** within it. Therefore attempting to make the model conform too closely to slight inaccuracies can **infect** the model with substantial errors and **reduce its predictave power**. 

##### Consequences:
Training error:
- The proportion of training records that are misclassified
- Overly optimistic. Overfitting can have poor accuracy on unseen data
- Error can be seen as opposite of Accuracy. 

---

### Good workflow for training/testing

1. Divide training set into training and **validation**
2. Train model on training set
3. Evaluate on validation set
4. Tweak model according to results (back to step 2)
5. Pick model that does best on validation set
6. Confirm results on test set

Data should always be split into training/validation/test.

**Training**: for model construction (65%)
**Validation**: for setting hyperparameters (15%)
**Testing**: for accuracy estimation (20%)

---

### Class Imbalance

Data with skewed class proportions is called **imballanced**. The larger proportion class is called *majority* class and the smaller, *minority* class. 

##### Solutions

**Downsampling**: training on a disproporionately low subset of the majority class examples (may lead to *underfitting*).

**Upsampling**: training on a disproportionately high subset of the minority class examples (may lead to *overfitting*)

---

### Ensemble Methods

Combining a set of hetrogeneous classifiers to increase accuracy.

Popular ensemble methods:

- Average the classifier scores
- **Weighted average of classifier scores**
- Bagging: averaging the prediction over a collection of classifiers
- Boosting: weighted vote with a collection of classifiers

---

### Ethics

Word embeddings can weight words associated with others. This can lead to issues as the word "women" is more weighted towards things like: "nanny", "receptionist" etc. Whereas "man" is more associated to "janitor", "referee", "actor", "plumber" etc.

This poses a significant risk and challenge for machine learning and applications.

### University Grades classifier

##### Issue 1: Different people, different mistakes

If university is male dominant, the classifier will be more used to classifying male work. Therefore may classify males 90% correctly but females only 50% correctly. To address this, the algorithm would need to be changed to care equally about accuracy for both men and women.

##### Issue 2: Historical Bias

If a university in the past has not admitted minorities. Then since the model is built on that historical data, it would give out the same bias, therefore algorithms objective would need changed.

##### Issues 3: Conflicting Priorities

No prediction system is perfect and that limitation will always affect some students more than others. If the accuracy is raised for some group, it will be lowered for another. Balancing these competing factors in a single mathematical objective is a complex issue of judgement with no single answer.

#### The 5 C's of Ethics

- Consent
- Clarity
- Consistency
- Control & Transparency
- Consequences & Harm


### Ethics: Summary

- Dont be focussed on performance towards a single objective - use multiple metrics
- Analyse failures
- Explainability - what features caused this failure
- Analyse decision bounds - do these feature boundaries make sense?
- Analyse unseen data from the population - is the traing data really representative?
- Analyse feature patterns - how removing this feature will change predictions
- Accountability - who will be blamed?
- Measure bias - evaluate the output for systematic bias
- **Ethical requirements should be considered at the design stage**
