# Decision-Tree

The purpose of this project was to get familiar with Classification and Regression Decision Trees (CART). i have applied the Regularization models on a dataset

**Decission Trees Classification.ipynb**: Decision Tree applied on a dataset whre the predictive feature is categorical
**Decission Trees Regression.ipynb**: Decistion Tree applied on a dataset where the predictive Feature is quantitative 

This notebook can be used as an good example to show other people how Decision Trees algorithms work

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Decision Trees**
- Highly interpretable, even more than KNN and Regression models
- Sequences of diferent quesitons
- Used for **Classification** and **Regression** problem statements

Decision Tree Definitions
- Decision Trees are Machine Learning algorithms that progressively divide data sets into smaller data groups based on descriptive feature, until they reach sets that are small enough to be described by some label
- Decision Trees apply a top-down approach to data, trying to group and label observations that are similar
- When the target variable consits of real numbers we use **Regression Trees**
- When the targes variable is categorical we use **Classification Trees**
- Terminology
    - Root node: Beginning of a tree
    - Spliiting: Splitting the tree
    - Branch: the branch that goes to the Decision node
    - Leaf node (Terminal node)
    - Sub-Tree
    - Depth-level (longest path from the Root node to the Leaf node)
    - Prunning (removing sub notes from a tree)
    
 **We can check the impurity of our Decision Tree with:**
- Regression Trees
    - MSE (Mean Squared Error)
- Classification Trees
    - Error Rate: probability of making a mistake
       - (perferably not used in practice as it is sensitive to overfitting the data)
    - Entropy: Measures the impurity of randowmness (uncertainty) in the data points
    - Gini Index: Measures how often a randomly chosen element would be incorrectly labeled
    
    
    
 Different decision tree algorithms utilize different impurity metrics
 
 **How does the algorithm select X(feature) and s (split)?**
 - Using Recursive Binary Splitting: This is a numerical procedure where all the values are linked up and different split points are tried and tested using a cost function. The split wiht the lowest cost is selected
 - Split that leads to the largest possible reduction in RSS (Residual Sum of Squares)
 - Calculatin with different lines where the MSE is the smallest
 - The algortihm repeates the process, looking for the best feature and best split in order to split the data further to minimize the RSS within each of the resulting regions
 - The process continues until a stopping criterion is reached; for instance, continues until no regeion contains more than a fixed number of observation
 
**Classification Trees**
- Classification trees are very ssimilar to regression trees, except that it is being used to predict a qualitative response rather than a quantitative one
- The prediction of the algorithm at each terminal node will be the category with the majority of datapoints i.e., the most commonly occuring class
- Just as in the regression, the recursive binary splitting is used to grow a classification tree. However, instead of RSS we will be using one of the following impurity criteria:
    - Classification error rate: Not sufficiently sensitive to node purity (changes in the node probabilities) and in practice either Gini or Cross Entropy is prefered 
    - Gini index: What features to start with and where to do the split
    - Cross entropy
    
**Pruning a tree*
- Decision Tree may produce good predcitions on the training set, but is likely to overfit the data leading to poor test performance (this is the result when no hyperparameter tuning is done as the Decision tree will make every possible split for every variable in the train set. Then applying this model on the test set will result in high Bias.
- Smaller tree with fewer splits may lead to lower variance and better interpretation at the cost of a litle bit of bias (This strategy may result in smaller trees, but is too short-sighted)
    - A seemingly worhtles split early on in the tree might be followed by a very goot spliy, a split that leads to a large reduction in RSS/impurity index later on
- Making all the decisions in the trees and then pruning back to the good trees
- A better strategy is to grow a very large tree, and then prune it back in order to obtain a subtree
- Cost complexity pruning is used to do this (penalizing by restricting adding more complexity to the model)

**Cost complexity pruning also called as weakest link pruning**
- Consider a sequence of trees indexed by a nonnegative tuning meter alpha(lambda)
- For each value of alpha corresponds a subtree such that the following objective functions is minimized
- Can find best alpha with cross validation (CV)
- Alpha control the bias variance trade off and is determined by cross validation (CV)

**Building a Regression Tree**
1. Use recursive binary splitting to grow a large tree (this is a numerical procedure where all the values are lined up and different split points are tried and tested using a cost function. The split with the lowest cost is selected)
2. Apply cost complexity to pruning to the large tree in order to obtain a sequence of best subtrees, as a function of alpha (lambda)
3. Use K-fold cross-validation (CV) to choose the best alpha (lambda). That is divide the training observations into K fold. For each k=1,..K: \
    a. Repeat steps 1 and 2 on all but the k fold of the training data\
    b. Evaluate the mean squared (MSE) prediction error on the data in the left out k fold, as a function of alpha. Average the results for each value of alpha, and pick alpha minimize the average error.\
4. Return the subtree from step 2 that corresponds to the chosen value of alpha


**Avoiding Overfitting**
To avoid overfitting, regularization parameters can be added to the model such as:
- Maximum depth of the tree: Maximum splits of a tree
- Minimum population at a node: Number of observations in the node (the minimum populationa node should consist of). if you don't use a number of observation your model will overfit
- Maximan number of decision nodes (amount of nodes you want to have)
- Minimum impurity decrease: info gain
- Alpha: Complexity parameter

Other **hyperparameters are**:
- Criterion
    - Gini
    - Entropy
- Splitter
    - Best
    - Random
- Class weight
 - Balanced
 - None 
 
 Imbalanced data typically refers to a classification problem where the number of observations per class is not equally distributed; often you will have a large amount of data/oberservations for one class(referd as the majority class which is overrepresented) and the smalles as the minority class
 
 **Decision Trees Pros and Cons**
- Pros
    - Easy to interpret and visualize
    - Can easily handle categorical data without the need to create dummy variables
    - Can easily capture Non-linear patters
    - Can handle data in its raw form (no preprocessing and Scaling needed as it does not use euclidience distance)
    - Has no assumptions about the distribution because of the non-parametric nature of the algorithm
- Cons
    - Poor level of predictive accuracy (This can be reduced by bagging and boosting algorithms)
    - Sensitive to noisy data. It can overfit noisy data. Small variations in data can result in different decision trees
       
**Overfitting, Underfitting and Fitting**

    - Overfitting = Bias low, Variance high
    - Underfiting = Bias high, Variance High
    - Fitting = Bias low, Variance low
