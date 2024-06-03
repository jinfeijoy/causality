## Causal Diagrams

#### Lesson 1: Causal DAGs
* [Ascertainment bias](https://catalogofbias.org/biases/ascertainment-bias/)
* DAG(Directed Acyclic Graph): 
  * If our expert knowledge is insufficient for us to rule out a direct effect of variable D on variable E, we should draw an arrow from D to E on the causal DAG. The absence of an arrow on a DAG means that we believe there is no relationship between D and E for each individual person in the population. Therefore, it is a stronger assumption to not have an arrow on a DAG, than to have one. As such, if we cannot rule out a direct effect of D on E, we should draw an arrow.
  * Flow Cause and Effect: A -> B -> Y
    * The flow of association between A and Y is interrupted when we condition on the mediator, B. The box around B blocks the association between A and Y. So if there is no direct arrow from A to Y, we say that there is no association between A and Y conditioned on B, even though A has a causal effect on Y.
    * Whether A and Y are associated conditional on B? We will check whether A contains information not already included in B that allows us to predict Y better.   
* Systematic bias: any association between A and Y that is not due to the effect of A and Y is considered a systematic bias.
  * Flow Common Causes: 
    * ![image](https://user-images.githubusercontent.com/16402963/147861907-0a064b3c-285c-4dfd-987b-ed329cc8e4ba.png)
    * We cannot exclude an association between A and Y when A and Y have a common cause, L, even if there is no arrow from A to Y.
    * Learning that someone has yellow fingers when we already know she's not a smoker does not provide any additional information regarding her risk of lung cancer.
    * The flow of association between A and Y is interrupted when we condition on their common cause, L. The box around L blocks the association between A and Y. So there is no arrow from A to Y, we say that there is no association between A and Y conditional on L.   
* Selection Bias: when there is a component of the association of these, due to selecting a subset of the population.
  * Flow Conditional on Common Effects: 
    * ![image](https://user-images.githubusercontent.com/16402963/147862156-c3fd9f27-71a5-4cbc-92ef-0778dfca4106.png) 
    * We cannot exclude an association between A and Y when A and Y have a common effect, L, and we condition on that common effect, even if there is no arrow from A to Y.
* D-separation: We use D-separation to decide whether two variables are D-separated, where D stands for directional.
  * If there are no variables being conditioned on, a path is blocked if and only if two arrowheads on the path collide at some variable on the path.
    * the path between A and Y is blocked: 
    * ![image](https://user-images.githubusercontent.com/16402963/147862600-c3918729-c487-44eb-8940-4c5d4fdecb7c.png) 
  * Any path that contains a noncollider that has been conditioned on is blocked.
    * the path between A and Y is blocked after conditional on B: 
    * ![image](https://user-images.githubusercontent.com/16402963/147862635-74d7f908-9730-4a6c-a9ef-80c3ae02e956.png) 
  * A collider that has been conditioned on does not block a path.
    * the path between A and Y is open after conditional on L: 
    * ![image](https://user-images.githubusercontent.com/16402963/147862651-228b7294-f210-4b63-af13-8728980262f0.png)
  * A collider that has a descendant that has been conditioned on does not block a path.
    * the path between A and Y is open after conditioning on S, which is a descendant of the collider L: 
    * ![image](https://user-images.githubusercontent.com/16402963/147862680-38aa88cb-3065-4ecc-b99f-457345eadc18.png)
  * **Summary**: a path is blocked if, and only if, it contains a noncollider that has been conditioned on, or a collider that has not been conditioned on and has no descendant that had been conditioned on.
  * All paths blocked = no association
  * D-separation = statistical independence

#### Lesson 2: Confounding
* Common Causes -- Confounding / System Bias
  * A and Y have a common cause, L. But there is no causal effect of A on Y. In this setting, all the association between A and Y is due to confounding.
* Backdoor path criterion
  * ![image](https://user-images.githubusercontent.com/16402963/147893119-40e3ebf2-1c20-4aa8-8ddd-1962b0774e4c.png) 
  * Definition: the path from A to L to Y is backdoor path.
  * Criterion: we can identify the causal effect of A and Y if we have sufficient data to block all backdoor paths between A and Y.
  * The backdoor path criterion answer two questions:
    * Can we identify the causal effect of interest?
    * What variables do I need to identify that effect? (which is to block all backdoor path to eliminate the confounding.
* Confounder: 
  * a variable that possibly together with other variables, can be used to block all backdoor paths between treatment and outcome.
  * variable is a confounder of the effect of A on Y if it meets three conditions. (Not always correct)
    * First, the variable has to be associated with treatment A. 
    * Second, the variable has to be associated with the outcome Y conditional within levels of treatment A. 
    * Third, the variable cannot be on a causal pathway from A to Y.
* In summary, in any given causal DAG confounding is an absolute concept, but confounder is a relative concept. Confounding either exists or doesn't exist, but the variable may or may not be a confounder, depending on which other variables are being adjusted for.
* Confounding Control:
  * Randomization
  * To adjust confounding when we only have observation data: 
    * measure enough variables to block all backdoor paths between A and Y
      * Stratification 
      * Matching /propensity score
      * G methods
        * inverse probability weighting
        * standardization (G-formula)
        * G-estimation
    * alternatives to blocking backdoor paths (e.g. instrumental variable estimation)
* we need expert knowledge to determine if we should adjust for a variable. The statistical criteria are insufficient to characterize confounding and confounders.

#### Lesson 3: Selection Bias
* Conditional on Common Effects -- Selection Bias: The bias that is introduced by conditioning on a collider is commonly referred to as selection bias.
* Selection Bias Other common names: inappropriate selection of controls, Berkson's bias, loss to follow-up, non-response bias, missing data bias, volunteer bias, self-selection bias, healthy worker effect, etc.
* selection bias under the null is also referred to as collider stratification bias.
* Selection bias arise for 2 reasons:
  * Eligibility Criteria
    * ![image](https://user-images.githubusercontent.com/16402963/147954777-1dcfd359-c284-4c6b-a59e-c936ca939eaa.png)
    * First, selection bias may arise because of the criteria used to decide who is initially included in the study, who is selected into the study.
    * selection bias under the null is caused by conditioning on a variable that is a common effect of a treatment or a cause of the treatment and of the outcome or a cause of the outcome.
  * Loss to follow-up
    * ![image](https://user-images.githubusercontent.com/16402963/147954826-6129c07f-1783-4130-a7df-fc1258d96ab9.png)
    * Second, selection bias may arise because individuals who met those eligibility criteria at baseline, then got lost during the study.
    * Randomization may be our best weapon against confounding at baseline, but it is powerless against biases like these selection bias that happen after baseline.
    * ![image](https://user-images.githubusercontent.com/16402963/147955556-b036efb7-cf59-42e1-ae42-21db5171c9fa.png)
* Selection Bias Control:
  * Smart Selection: selecting controls independently of treatment, more generally we want to avoid selecting on colliders or their descendants
  * Adjust for selection bias: consider the backdoor paths between selection C and outcome Y rather than the backdoor between treatment A and the outcome Y.
    * Stratification: In order to use stratification to adjust for selection bias, we need data on all the variables that are required to block all the backdoor paths between the collider and the outcome.
      * Restriction
      * Pooling stratum-specific estimates
    * Inverse Probability Weighting (resampling by the weighting): requires 2 things:
      * knowledge about the true casual DAG
      * data on the variables that need to be adjusted for
  
#### Lesson 4: Measurement Bias/Putting it all together
* Measurement bias (information bias): When the association between A-star and Y-star differs from the association between A and Y.
  * ![image](https://user-images.githubusercontent.com/16402963/147984032-827dc803-383d-4cff-97c0-6b3e589fa150.png)
  * A: True treatment, A*: observed treatment, Y: true outcome, Y*: observed outcome, U-sub-A: all factors other than A, U-sub-Y: all factors other than Y.
* Measurement bias types:
  * **independent non-differential**: No bias under the null (when the effect of A on Y is null, the association between A star and Y star is also guaranteed to be null.)
  * dependent non-differential.
  * independent differential.
  * dependent differential.
  * ![image](https://user-images.githubusercontent.com/16402963/147989934-40973b8e-0960-4a9b-946a-49e62d46bb77.png)
* A paradox seems to exist only when the problem is stripped of its causal context, and analyzed merely in statistical terms.
* Challenges: 
  * Insufficient data
  * Wrong population
  * Measurement error
  * Selection Bias
  * Confounding 

#### Lesson 5: Time-Varying Treatments
* on heart disease, cholesterol level is the time-varying confounder affected by prior treatment. In studies of treatments for diabetes, glucose level is a time-varying confounder affected by previous treatment. In all these cases, conventional methods may yield biased effect estimates, even if all time-fix and time-varying confounders are correctly measured.
* for confounding adjustment-- decertification, outcome progression, matching, etc. None of these methods can handle time-variant confounders when there is treatment-confounder feedback because all these methods estimate associations within levels of the time-variant confounders. More general methods can handle this setting. These methods are known as g-methods.

#### Lesson 6: Causal single world intervention graphs (SWIGs)
* exchangeability
  * In the language of causal DAGs, exchangeability means that there are no common causes between treatment A and outcome Y.
  * Randomization makes the groups exchangeable. And this exchangeability of the treated and the untreated is the condition that we need to interpret association as causation.  
  * ![image](https://user-images.githubusercontent.com/16402963/148152391-030d4c4b-926b-4d77-a803-c22b225cc22c.png)
  * SWIGs: ![image](https://user-images.githubusercontent.com/16402963/148153211-20c27c04-888d-4d8a-a80d-3f7c78288aff.png)
    * the path between the treatment A and the counterfactual outcome is now blocked by the vertical line |.

#### Lesson 7: Building Your DAG
* For random trail, we don't need to add more variables to A->Y diagrams, Adding the causes of Y is not necessary because they are not causes of A and Y
* For observed data, we need to add the common causes of every pair of variables in the DAG. typically L for measured, U for unmeasured.
* Selection node also can be added for right censored data.
* Measurement error node can be added to DAG
* when drawing causal DAGs, we don't need to include all variables. we only need to include the treatment, the outcome, the selection nodes, in some case the mediators, sometimes the measurement error, and always the common causes of any pair of variables in the graph.
* An approach to causal discovery is based on exploiting the presence or absence of conditional independences in the data.


#### Case Study
* Birth Weight Paradox
  * ![image (4)](https://user-images.githubusercontent.com/16402963/148480547-5bdfa6f5-c34e-43dc-83c6-518aba5bb3f5.jpg)
  * ![image](https://user-images.githubusercontent.com/16402963/148480625-609ed5d7-032c-41bf-9aa8-7a720aadf22e.png)
* Measurement Bias in Memory Loss
* Confounding in mediation analysis
  * the standard approach to mediation analysis and muchepidemiologic and social science research,and in both observational studies and in randomized trials,consist first of regressing an outcome Y on the treatment variable Aand possibly also some covariates C.
  * Difference Method
    * ![image](https://user-images.githubusercontent.com/16402963/148613693-8c46d68c-be44-48b7-b40b-961b933e04e3.png)
    * We then see if adding the mediator to the regression modelchanges the coefficient for the effect of treatment.If the effect of treatment goes down a lotwhen we put the mediator in the regression model,then we think some of the effect must be mediated or explained by the mediator.
  * Product Method
    * ![image](https://user-images.githubusercontent.com/16402963/148613883-bf7c9f36-f5e5-44fe-b02c-358ba12ab09d.png)
  * However, for these method, they have strong assumption, which is about confounding. We randomize the trail, but we havn't randomize the mediator. so to get estimates of direct and indirect effects, we need to worry about confounding of the effect on the mediator on the outcome.
    * We need to control for possible confounders or common causesof that relationship between the mediator and the outcometo get valid estimates of direct and indirect effects. We need to do that even if we have randomized the exposure.
  * ![image](https://user-images.githubusercontent.com/16402963/148615440-91bc8789-3387-4776-bc42-6d8623c4de48.png)
    * We've randomized A, but we've not randomized M, our mediator-- antidepressant use.And so we want to add to that diagram potential mediator outcome confounders, common causes of M and Y, which we denote by C.And the assumption in a randomized trial to assess direct and indirect effects is that our baseline covariate C suffice to control for that mediator outcome confounding.
    * if we don't control for that mediator outcome confounder-- our estimates of direct and indirect effects will be biased: selection bias due to conditioning on a collider.
    * we need to think carefully about mediator outcome confounding, about what the mediator outcome confounding variables might be, about trying to collect data on them, and about controlling for them in the analysis, and then when the analysis is complete, using sensitivity analysis techniques to assess robustness to unmeasured mediator outcome confounding.
* Genes as Instrumental Variables
  * ![image (5)](https://user-images.githubusercontent.com/16402963/148705638-ae3db618-6d61-4bb9-a80b-ba6f91e17f11.jpg) 
* The Obesity Paradox
  * Say you have a clinical cohort, maybe a diabetes clinic or a heart failure clinic. You measure the weight of the patients, and you often find that the heavier patients, the obese patients, do better. They survive longer or they have a more benign course of illness than the leaner patients. That's what we call the obesity paradox.
  * ![image](https://user-images.githubusercontent.com/16402963/148705407-99ffded7-184d-4723-81bc-218ee1748369.png)
    * The implication of this structure is that if you observe the relationship between obesity and mortality within this selected sub-population, it will look protective even though it's not actually beneficial for any individual in the population.
  * ![image](https://user-images.githubusercontent.com/16402963/148705418-dfcc9ab4-24b3-4dce-9530-e7815cd2c803.png)
    * appearing ill and being obese are independent in the source population. In reality, they're probably negatively correlated because kids with type 1 diabetes are likely to lose weight. But even if they were independent, the collider-stratification bias that's created by this study design is going to generate a negative correlation between those nodes. And if a negative correlation actually existed, it would be distorted and made even more negative. This is because if the kids didn't arrive at the A1C test in their medical record through one pathway, they were more likely to arrive through the other pathway. It's not necessary that obesity actually be protective therefore to generate the protective association in the analysis. It just needs to be the less common way of having diabetes in this data set among the kids who have the test.
  * Inverse probability of censoring weighting is a very simple way to make an adjustment that tries to replicate what you would have observed in the unselected population.
  * it's always good to think about sensitivity analyses. Think about variables that you didn't measure, other improprieties in the analysis, things that you want to examine to see how far off you could be. And this can be done with simulations and bias formulas.
  * **It's important to draw the assumption before drawing the conclusion**
