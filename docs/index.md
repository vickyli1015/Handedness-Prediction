<h1>Predicting Handedness with Resting-State fMRI</h1>
  
By: Vicky Li, Anastasiya Markova, Zhuoxuan Ju; 
Mentors: Armin Schwartzman, Gabriel Riegner


<h2>Introduction</h2>

Lateralization refers to the specialization of certain brain functions to specific hemispheres, with handedness being one of the most well-documented examples. Brain activity during task-based experiments, such as language tasks, has exhibited strong lateralization patterns correlated with handedness (Pujol et al., 1999). Right-handed individuals make up approximately 90% of the population, while left-handed individuals account for only 10% (Coren & Porac, 1977). Given this distribution, much of the existing research focuses on right-handed individuals, and this could lead to generalized assumptions that may not fully capture differences for left-handed individuals.
As a result, our problem statement is: Do significant brain asymmetries, which influence lateralization and handedness, only emerge in task-based conditions, or can they also be detected in resting-state functional connectivity? With machine learning techniques, we aim to classify individuals as left- or right-handed based solely on their resting-state fMRI signals. While previous studies have investigated this classification, we will investigate functional connectivity on data that reflect hemispheric separations and data that doesn’t. Our goal is to build upon existing findings, assess whether resting-state connectivity alone can predict handedness, and how big of a role connectivity between hemispheres plays in these predictions.

Have you ever wondered if your brain "knows" whether you're left-handed or right-handed—without you even moving a finger? Turns out, it might!

Most research on handedness (which hand you prefer to use) looks at how the brain works during tasks, like writing or grabbing an object (Pujol et al., 1999). But what if we could predict handedness just from brain activity when you're doing nothing at all?

That’s exactly what we set out to explore! Using resting-state fMRI (a brain scan taken while people are simply lying still), we applied machine learning to see if brain connectivity alone can reveal whether someone is left- or right-handed.

We also wanted to dig deeper:

<p> Can certain brain regions tell us more about handedness than others? </p>
<p>· Does communication between the two hemispheres play a role? </p>
<p>· And most importantly—how well can a computer predict handedness from brain connections alone? </p>

<h2>Data</h2>

We used brain scan data from the Human Connectome Project (HCP), which has fMRI recordings from 1003 subjects. Each person’s scan captured one hour of brain activity while they were at rest—no thinking, no moving, just the brain doing its thing.

<h3>How is the brain data organized?<h3>
Imagine the brain as a giant network of interconnected regions. We studied two different ways to divide it:

1. ICA Parcellation (300 Regions):
Groups brain activity based on signal patterns, not physical location.
Regions might spread across both hemispheres.
Useful for broad connectivity patterns.
2. CA Parcellation (718 Regions):
Separates the brain into specific anatomical areas (left vs. right hemisphere).
Helps study how connectivity between hemispheres affects handedness.
To understand handedness, we used scores from the Edinburgh Handedness Inventory (EHI), a questionnaire that asks about daily tasks like writing, throwing, and using utensils.

A score above 0 means right-handed ✍️
A score below 0 means left-handed 🖊️
A score of 0? Ambidextrous! 🎭
Balancing the Data ⚖️
There’s a catch: Most people (about 90%) are right-handed, which makes lefties a rare find in our dataset.

ICA Data (All subjects): 912 righties, 88 lefties, 3 ambidextrous
CA Data (Subset of 165 subjects): 12 lefties, 153 righties
To prevent our machine learning models from being biased toward right-handers, we used a technique called SMOTE (Synthetic Minority Oversampling Technique) to create synthetic left-handed data points based on real ones—helping balance things out for fairer predictions.

<h2>Methods</h2>

<h2>Results</h2>

<h2>Conclusion</h2>

<h2>Reference</h2>
