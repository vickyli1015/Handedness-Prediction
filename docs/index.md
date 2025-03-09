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

I think here we can put the plot of the correlation matrice generation process we use for the poster, as well as the process diagram we have in the poster.

<hr>

<h2>Results</h2>

We can have the plots from the poster

<hr>

<h2>Conclusion</h2>

<hr>

<h2>Reference</h2>
