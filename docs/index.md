<h1>Predicting Handedness with Resting-State fMRI</h1>
  
By: Vicky Li, Anastasiya Markova, Zhuoxuan Ju; 
Mentors: Armin Schwartzman, Gabriel Riegner


<h2>Introduction</h2>

<p>Have you ever wondered if your brain “knows” whether you’re left-handed or right-handed—without you even moving a finger? Turns out, it might!</p>

<p>Most research on handedness looks at brain activity during <b>task-based experiments</b> (like writing or grabbing an object) (put reference here!). But what if we could predict handedness <b>just from brain activity when you’re doing nothing at all</b>? That’s exactly what we set out to explore.</p>

<p>Using <b>resting-state fMRI</b> (a brain scan taken while people are simply lying still), we applied <b>machine learning</b> to see if brain connectivity alone can reveal whether someone is left- or right-handed.</p>

<h3>Using machine learning models, we investigated:</h3>
<ul>
  <li>Whether functional brain connectivity patterns differ between left- and right-handed individuals</li>
  <li>The role of interhemispheric connectivity in these predictions</li>
  <li>How well different machine learning models perform in classifying or predicting handedness based on brain connectivity</li>
</ul>

<hr>

<h2>Data</h2>
<p>We used brain scan data from the <b>Human Connectome Project (HCP)</b>, which has fMRI recordings from <b>1003 subjects</b>. Each person’s scan captured <b>one hour</b> of brain activity while they were at rest—no thinking, no moving, just the brain doing its thing.</p>

<h3>How is the brain data organized?</h3>
<p>Imagine the brain as a giant network of interconnected regions. We studied two different ways to divide it:</p>

  <ul>
  <li><b>ICA Parcellation (300 Regions):</b>
    <ul>
      <li>Groups brain activity <b>based on signal patterns</b>, not physical location.</li>
      <li>Regions might spread across both hemispheres.</li>
      <li>Useful for broad connectivity patterns.</li>
      <li>Here we can put the interactive plot/plot that shows how ICA parcellation looks like.</li>
    </ul>
  </li>

  <li><b>CA Parcellation (718 Regions):</b>
    <ul>
      <li>Divides the brain into <b>specific anatomical areas</b> (left vs. right hemisphere).</li>
      <li>Helps study how connectivity between hemispheres affects handedness.</li>
      <li>Here we can put the interactive plot/plot that shows how CA parcellation looks like.</li>
    </ul>
  </li>
</ul>


<h3>How do we measure handedness?</h3>
<p>We used the <b>Edinburgh Handedness Inventory (EHI)</b>, a questionnaire that asks about daily tasks like writing, throwing, and using utensils.</p>
<ul>
  <li><b>Score > 0:</b> Right-handed </li>
  <li><b>Score < 0:</b> Left-handed </li>
  <li><b>Score = 0:</b> Ambidextrous </li>
</ul>

<h3>Balancing the Data ⚖</h3>
<p>There’s a catch: Most people (about <b>90%</b>) (we need reference here!) are right-handed, which makes lefties <b>a rare find</b> in our dataset.</p>

<ul>
  <li><b>ICA Data (All subjects):</b> 88 left-handers, 912 right-handers, 3 ambidextrous</li>
  <li><b>CA Data (Subset of 165 subjects):</b> 12 left-handers, 153 right-handers</li>
</ul>

<p>To prevent our machine learning models from being biased toward right-handers, we used a technique called <b>SMOTE (Synthetic Minority Oversampling Technique)</b> to create <b>synthetic left-handed data points</b> based on the real data points to generate synthetic samples for the minority class to improve model balance and performance. </p>

<hr>

<h2>Methods</h2>

  <p>I think here we can put the plot of the correlation matrice generation process we use for the poster, as well as the process diagram we have in the poster. (will be removed in final version)</p>


  <p>Handedness can be viewed as binary, left or right-handed, as well as continuous based on the Edinburgh Handedness Index. This led us to explore two types of models: regression and classification.</p>
    
  <p>Both models utilize functional connectivity, which we calculated through partial correlation matrices for each subject. For the CA data, the correlation matrix was 718 by 718, corresponding to all possible pairs between 718 regions. For the All ICA and Matched ICA data, the correlation matrices were 300 by 300, corresponding to 300 regions used. We applied Fisher Z-transformation to normalize the correlations.</p>

  <p>Every value inside the correlation matrix is the correlation between two brain regions which forms an edge. We can now think of every value in the correlation matrix representing an edge. We computed the correlation between a particular edge across all subjects and the corresponding handedness scores. Top n number of absolute strongest correlations were used as inputs into the model. The appropriate number of n edges was selected via grid search. </p>
    
<h3>Classification</h3>
  <p>For classification, we used a model that always predicts mode as our baseline. The balanced accuracy score was used for evaluation, with a baseline score of 0.5.</p>
    
  <p>Since left-handed people make up less than 10% of our dataset, we used the Synthetic Minority Oversampling Technique (SMOTE) to rebalance the dataset. This technique uses a nearest neighbors approach. It takes a point, finds k nearest neighbors, randomly selects one of the nearest neighbors, and adds a point on the linear path between our point and the random neighbor we chose. We then separate our balanced dataset into 25% test and 75% train sets. </p>

  <p>We implemented K-Nearest Neighbors (KNN) classifiers first, and performed grid search to identify the hyperparameters which correspond to the best balanced accuracy score. 
</p>

    
<h4>K-Nearest Neighbors (KNN) Classifier</h4>
  <table>
      <tr>
          <th>Dataset</th>
          <th>Number of Edges</th>
          <th>Value of k</th>
          <th>Accuracy</th>
      </tr>
      <tr>
          <td>Matched ICA</td>
          <td>60</td>
          <td>3</td>
          <td>1.00</td>
      </tr>
      <tr>
          <td>CA Data</td>
          <td>15</td>
          <td>3</td>
          <td>0.99</td>
      </tr>
      <tr>
          <td>All ICA</td>
          <td>5</td>
          <td>3</td>
          <td>0.95</td>
      </tr>
  </table>
  
<h4>Support Vector Classifier (SVC)</h4>
  <p>Then we implemented a Support Vector Classifier (SVC), and performed a similar grid search of the hyperparameters. After trying <b>linear</b>, <b>poly</b>, <b>rbf</b>, <b>sigmoid</b> kernels, only the sigmoid kernel produced reliably stable results, so it was chosen for the model.</p>

  <p align="center">
  <img src="../images/knn.png">
  </p>


  <p>where the kernel coefficient `alpha` controls the influence of each training sample on the decision boundary and is the bias term <b>c</b> that shifts the data up or down.
</p>

  <p>In the sigmoid kernel, the similarity between two data points is computed using the hyperbolic tangent function <b>tanh</b>. The kernel function scales and possibly shifts the dot product of the two points <b>x</b> and <b>y</b>.
</p>
  
  <p>After testing different kernels, the sigmoid kernel was chosen for stability.</p>
  <table>
      <tr>
          <th>Dataset</th>
          <th>Number of Edges</th>
          <th>Accuracy</th>
      </tr>
      <tr>
          <td>Matched ICA</td>
          <td>68</td>
          <td>1.00</td>
      </tr>
      <tr>
          <td>CA Data</td>
          <td>72</td>
          <td>1.00</td>
      </tr>
      <tr>
          <td>All ICA</td>
          <td>60</td>
          <td>0.94</td>
      </tr>
  </table>

  <p>When analyzing the performance, we ran each model 500 times on different train-test splits to make sure that our results are consistent. We will be reporting average balanced accuracy across 500 trials in our results.</p>
  <p>In order to achieve a greater level of explainability, since the sigmoid kernel is hard to interpret, permutation testing was conducted to evaluate the importance of each feature passed into the model. We first conducted hierarchical clustering to filter out features that are correlated with each other, and reduce multicollinearity within the dataset. First, we extracted our features, which are the values of the edges across all subjects. Then, we compute Spearman correlation between multiple edges. Spearman correlation assesses whether the relationship between two variables can be described using a monotonic function, a function that preserves or reverses the order of the given order. This will help us reduce the number of input edges, since many of them follow the same pattern. Then, the distance matrix is computed using 1 - abs(corr), such that if the spearman correlation coefficient was high, close to 1 or -1, the distance would be small, close to 0. Then, we use Ward's method for hierarchical clustering, which minimizes the variance within clusters. In order to appropriately threshold hierarchical clustering, we computed a grid search using the following objective function. </p>

  <p align="center">
  <img src="../images/svc.png">
  </p>


  <p>The goal of this function was to maximize the balanced accuracy of the model as well as maximize the threshold. This way we are searching for the minimal number of edges while still achieving maximum accuracy. Once we selected the threshold, we filtered the features such that only one feature from every cluster is included in the model. Then, permutation testing was conducted to assess how significantly each feature affects the model. The permutation test shuffles the values of a specific feature, and assesses by how much the model performance decreased on average across multiple iterations. Through these processes we were able to assess  which brain regions most significantly impact the performance of our model.</p>
    
<h3>Regression</h3>
  <p>For regression, we aimed to predict handedness as a continuous variable ranging from -100 to +100 using connectivity features. Same as with classification, the inputs into our model were the edge values across all subjects. We used a model that always predicts the mean as our baseline. We use the evaluation technique of Root Mean Squared Error (RMSE), which is the square root of the mean squared difference between true and predicted values. We looked for an RMSE lower than the baseline model when creating new models.
</p>
    
  <h4>K-Nearest Neighbors Regressor</h4>
  <p>We started by applying the K-Nearest Neighbors Regressor. Similar to classification, we performed grid search to look for the optimal number of  edges and k values to include in our model.
</p>
  <table>
      <tr>
          <th>Dataset</th>
          <th>Number of Edges</th>
          <th>k</th>
          <th>RMSE</th>
      </tr>
      <tr>
          <td>Matched ICA</td>
          <td>130</td>
          <td>4</td>
          <td>20.9</td>
      </tr>
      <tr>
          <td>CA Data</td>
          <td>50</td>
          <td>4</td>
          <td>17.8</td>
      </tr>
      <tr>
          <td>All ICA</td>
          <td>40</td>
          <td>10</td>
          <td>38.13</td>
      </tr>
  </table>
  
  <h4>Spectral Embedding</h4>
  <p>Our second model is Spectral Embedding, which works by computing the graph Laplacian of a similarity matrix derived from the data, performing an eigenvalue decomposition, and selecting the eigenvectors associated with the smallest eigenvalues. These eigenvectors form the new lower-dimensional coordinates for the data, capturing the essential structure of the dataset in fewer dimensions. Since the Laplacian matrix depends on the similarity matrix, we have to apply it to the whole dataset rather than splitting it into a train and test set. We applied spectral embedding to reduce our dimensionality to just one or two dimensions. When Spectral embedding reduced our data to two dimensions, Principal Component Analysis was used to further reduce it to a single dimension and then apply linear regression where x are spectrally embedded values, while y are handedness scores.
</p>


<hr>

<h2>Results</h2>

We can have the plots from the poster

<hr>

<h2>Conclusion</h2>

<hr>

<h2>Reference</h2>
