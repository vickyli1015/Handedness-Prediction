<h1>Predicting Handedness with Resting-State fMRI</h1>
  
By: Vicky Li, Anastasiya Markova, Zhuoxuan Ju; 
Mentors: Armin Schwartzman, Gabriel Riegner


<h2>Introduction</h2>

<p>Have you ever wondered if your brain “knows” whether you’re left-handed or right-handed—without you even moving a finger? Turns out, it might!</p>

<p>Most research on handedness looks at brain activity during <b>task-based experiments</b> (like writing or grabbing an object). But what if we could predict handedness <b>just from brain activity when you’re doing nothing at all</b>? That’s exactly what we set out to explore.</p>

<p>Using <b>resting-state fMRI</b> (a brain scan taken while people are simply lying still), we applied <b>machine learning</b> to see if brain connectivity alone can reveal whether someone is left- or right-handed.</p>

<h3>What are we trying to find out?</h3>
<ul>
  <li>Can certain brain regions tell us more about handedness than others?</li>
  <li>Does communication <b>between</b> the two hemispheres play a role?</li>
  <li>How well can a computer predict handedness based on functional connectivity?</li>
</ul>

<p>Let’s dive in and find out! 🚀</p>
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
    </ul>
  </li>
  <li><b>CA Parcellation (718 Regions):</b>
    <ul>
      <li>Divides the brain into <b>specific anatomical areas</b> (left vs. right hemisphere).</li>
      <li>Helps study how connectivity between hemispheres affects handedness.</li>
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

<h3>Balancing the Data ⚖️</h3>
<p>There’s a catch: Most people (about <b>90%</b>) are right-handed, which makes lefties <b>a rare find</b> in our dataset.</p>

<ul>
  <li><b>ICA Data (All subjects):</b> 912 righties, 88 lefties, 3 ambidextrous</li>
  <li><b>CA Data (Subset of 165 subjects):</b> 12 lefties, 153 righties</li>
</ul>

<p>To prevent our machine learning models from being biased toward right-handers, we used a technique called <b>SMOTE (Synthetic Minority Oversampling Technique)</b> to create <b>synthetic left-handed data points</b> based on real ones—helping balance things out for fairer predictions.</p>

<h2>Methods</h2>

<h2>Results</h2>

<h2>Conclusion</h2>

<h2>Reference</h2>
