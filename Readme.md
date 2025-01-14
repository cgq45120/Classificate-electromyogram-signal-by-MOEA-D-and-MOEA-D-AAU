<font face="Times new Roman">

# Multichannel optimization for electromyogram signal with complex features in decomposition-based multi-objective evolution framework with adaptive angle selection<br>
## Introduction<br>
&emsp; Human electrophysiological signals are direct responses to human behavioral intention, and analysis and interpretation of human electrophysiological signal enable a machine to recognize effectively subjective awareness of a person. As one type of human electrophysiological signal, surface electromyogram (sEMG) signal contains information about muscle state and human motion intent, and applying gesture action recognition technique to intelligent prosthesis is not only able to assist patients losing arms in rehabilitation trainings but also able to make them have a “phantom limb feel”, so sEMG-based hand action recognition technique has important medical application value.<br>

&emsp; Current studies focus on the classification of a single objective (recognition accuracy), that is, this technique is considered as a single objective problem. In actual EMG signal application modeling, multiple factors such as recognition correctness, stability, and continuity should be taken into account together.<br>

&emsp; Under the MOEA/D algorithm framework, an algorithm for solving multi-objective EMG signal recognition problem was designed in this study.

## Model<br>
-------------
![Illustrations of the acute angle between solutions and corresponding weight vector](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/Illustrations_AU.png)

&emsp;Compared with MOEA/D, this algorithm changes how to choose which solution is better. solution A is the current solution and aa is the corresponding direction vector, &theta; is the acute angle between solution A and its corresponding direction vector aa, when the weighted Tchebycheff approach is used, which also is the acute angle between vector aa and vector F(x)−Z.

&emsp;According to the value of acute angle  &theta;(x) ,the smaller value of  &theta;(x),the closer the solution x to the direction vector aa. Thus, the solution which is close to the direction vector could be selected.

&emsp;The parameter G is the number of selected angles, which should be smaller and larger with evolution. The dynamic adjustment strategy adopted is to gradually increase the angle control parameter G in MOEA/D-AAU algorithm with evolution.

![sigmoid](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/sigmoid.png)

&emsp;Where Gmax is the maximum of Gr, and Gr is the value of G at present. S is the number of iteration times at present, S is the maximum of iteration times, y &in;[0,1) is a control variable parameter which used to control the growth rate of Gr.

&emsp;However, while screening the solutions this way, the algorithm may ignore some specific optimal solutions, so a global margin ranking strategy was introduced to build an external file set and rank updated solutions and original solutions based on individual margin information, resulting in individual dominance values (rank values) in solution space, then partial solutions are retained.

![GMR](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/GMR.png)

&emsp;where xi and xj are two mutually different individuals in the space, M is number of objectives, D(xi) is global density information of indivisual xi, dij is the Euclidean distance between individual i and individual j, GMR(xi) is global margin rank of individual xi, and GGR(xi) is global general rank of individual xi. From perspective of Pareto dominant concept, a smaller GMR(xi) indicates that individual xi dominates more other individuals. Degree of aggregation of individuals in solution space is measured using Euclidean distances of an individual from remaining individuals in the population and behavior of the individual so as to reduce effectively the impact of any extreme point or “outlier” on individual aggregation. Their combination results in global general rank (GGR), and a smaller GGR indicates that the individual is more dominant and that the individual density is small with good distribution.

The framework of proposed MOEA/D-AAU-GMR
-------------
![Framework of MOEA/D-AAU-GMR](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/Framework-of-MOEAD-AAU-GMR.png)
-------------
![Population Replacement of MOEA/D-AAU-GMR](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/Population-Replacement-of-MOEAD-AAU-GMR.png)
-------------
![Update external archive of MOEA/D-AAU-GMR](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/Update-external-archive-of-MOEAD-AAU-GMR.png)
-------------

## Multi-objective modeling of electromyogram signal recognition

![Multi-objective modeling](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/multi_objective.png)
<br>

&emsp;While minimizing numbers of channels and features, a high recognition efficiency should be guaranteed and excessively great difference in recognition accuracy between actions should be prevented

## part of result

![Result of objectives for MOEA/D-AAU](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/Result.png)
<br>

&emsp;As can be seen from the figure, the differences between the upper and lower bounds of accuracy vary with selected number of channels and number of features. Recognition using some features was likely to attain worse results. Average recognition accuracy of all experimentally obtained channel feature solutions was above 95%.
&emsp;From perspective of the test results, action accuracy variances were small and basically around 0.02, indicating that information of EMG signal can be effectively extracted from selected features and channels so as to recognize each action; furthermore, recognition accuracy of each action was high, and in some circumstances, cactions had been 99.9% accurate on average.
&emsp;Analysis of all obtained channel feature solutions resulted in the following information of usage of features and channels

![Distribution of feature usage rate](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/feature.png)
<br>

![Distribution of channel usage rate](https://github.com/cgq45120/Classificate-electromyogram-signal-by-MOEAD-AAU-GMR/blob/master/picture/channal.png)
<br>

&emsp;It can be found from Figs, usage rate of feature ZC (frequency of curves crossing zero, i.e., ZC, mainly reflects changing characteristics of different frequency components of sEMG signal) was 90.9%, much higher than that of any other feature, followed by usage rates of features RMS, FR, and IEMG, which were 43.4%, 52.1%, and 43.3%, respectively. The channels ranking top six in usage rate are Channels 1, 2, 8, 10, 12, and 16, respectively, with their usage rates being 67.1%, 65.7%, 68.5%, 62.2%, 57.6%, and 80.4%, respectively.
Compared with other features, ZC represents the frequency of sEMG signal magnitude crossing zero magnitude level and reflects degree of variation of sEMG signal, an increase in ZC indicates more high-frequency components in EMG signal while a decrease in ZC indicates more low-frequency components, so ZC is mainly an indication of changing feature of each frequency component in sEMG signal. EMG signal per site varies constantly with time, and different actions need different myofiber sites, thus differentiation in high-frequency or low-frequency component between channels becomes significant, and critical information can be better acquired with a classifier from frequency components of different channels of each action so as to discriminate actions, so selection rate of ZC feature will become very high.
