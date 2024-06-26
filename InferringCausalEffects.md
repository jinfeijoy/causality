# Inferring Causal Effects

* [Notes by T Yun](https://tyun.io/p/causal-inference-course-note1/)

## Week1
* Confusion over Causality
  * The field of causal inference or causal modeling attempts to do this by proposing:
     * formal definitions of causal effects
     * assumptions necessary to identify causal effects from data
     * rules about what variables need to be controlled for
     * sensitivity analyses to determine the impact of violations of assupmtions on conclusions 
  * A brief history
     * re-introduction of potential outcomes; Rubin causal model (Rubin 1974)
     * Causal diagrams (Greenland and Robins 1986; Pearl 2000)
     * Propensity scores (Rosenbaum and Rubin 1983)
     * Time-dependent confounding (Robins 1986; Robins 1997)
     * Optimal dynamic treatment strategies (Nurphy 2003; Robins 2004)
     * Targeted Learning (van der Laan 2009) 
* Causal Effect
  * we will primarily focus on treatments/exposures that could be thought of as interventions: treatments that we can imagine being randomized (manipulated) in a hypothetical trial
     * there are, of course, causal effects of variables like age, race, gender, and obesity, but they do not fit as cleanly in the potential outcomes framework
     * we focus on causal effects of hypothetical interventions because: their meaning is well defined / potentially actionable   
  * Average causal effect
     * E(Y1-Y0)
        * average value of Y if everyone was treated with A=1 minus the average value of Y if everyone was treated with A=0
        * if Y is binary this is a risk difference 
     * hard to get result based on single treatment, so can use average to represent causal effect 
  * Conditioning Versus Setting
     * E(Y|A=1):means of Y among people with A=1
     * E(Y1): means of Y if the whole population was treated with A=1
     * E(Y|A=1)-E(Y|A=0) is generally NOT a causal effect, because it is comparing two different populations of people.
     * E(Y1-Y0) is a causal effect, because it is comparing what would happen if the same people were treated with A=1 versus if the same people were treated with A=0 
  * Other causal effects:
     * E(Y1/Y0): causal relative risk
     * E(Y1-Y0|A=1): causal effect of treatment on the treated
        * might be interested in how well treatment works amoung treated people 
     * E(Y1-Y0|V=v): average causal effect in the subpopulation with covariate V=v
  * Challange:
     * How do we use observed data to link observed outcomes to potential outcomes
     * What assumptions are necessary to estimate causal effects from observed data 
* Causal Assumptions
   * Stable Unit Treatment Value Assumption (SUTVA): allows us to write potential outcome for the ith person in terms of only that person's treatments
      * No interference:
         * units do not interfere with each other
         * treatment assignment of one unit does not affect that outcome of another unit
         * spillover or contagion are also terms of interference 
      * One version of treatment
        
   * Consistency
      * The potential outcome under treatment A=a, Ya, is equal to the observed outcome if the actual treatment received is A=a:
         * Y = Ya if A = a for all a 
   * Ignorability
      * Given pre-treatment covariates X, treatment assignment is independent from the potential outcomes
         * among people with the same values of X, we can think of treatment A as being randomly assigned 
      * Observed data and potential outcomes
         * we can put those assumptions together to identify causal effects
         * E(Y|A=a,X=x) involves only observed data
         * E(Y|A=a,X=x) = E(Ya|A=a,X=a) (by consistency) = E(Ya|X=x) (by ignorability)
         * if we want a marginal causal effect, we can average over X
   * Positivity
      * for every set of values for X, treatment assignment was not deterministic:
         * P(A=a|X=x)>0 for all a and x
      * if for some value of X, treatment was deterministic, then we would have no observed value of Y for one of the treatment groups for those values of X.
      * Variability in treatment assignment is important for identification. 
* Stratification
   * Standardization example
      * compute rate of MACE for saxagliptin and sitagliptin initiators in two subpopulations
         * patients who have had no prior OAD use
         * pations who have had OAD use
      * then take weighted average, where weights are based on proportion of people in each subpopulation
      * This is a causal effect if, within levels of the prior OAD use variable, treatment can be thought of as randomized (ignorability given prior OAD use)   
   * Conditioning and marginalizing
      * under certain assumptions: E(Y|A=a, X=x) = E(Ya|X=x)
      * if we want a marginal causal effect, we can average over the distribution of X, suppose there is a single categorical X variable, then, E(Ya) = SUM E(Y|A=a,X=x)P(X=x) 
*  Incident user and active comparator design
   * example as to estimate taking yoga's impact to blood presure, to design the event, taking snapshot will lose the information that people take yoga before centain period and then stop. in this case, we need to pick the data point that people initial yoga as first time, it's easy to find out cut-off time for active event, but it's hard to define time for non-active user (group of people not taking yoga class). In this case, we may need to find other active comparator, i.e. take zomba class. By doing so, the design will change and narrow.
   * Other considerations
      * It is not always possible to implement an incident user design (e.g. causal effect of air pollution)
      * sometimes no treatment (unexposed) is the comparison group of interest
      * in this lecture we have focused design issues on the causal effect of the decision to initiate a treatment
        * causal methods exist that can handle time-varying treatments (causal effect of treatment regimens over time  

## Week2
* Confounding
   * Confounder control: we are interested in:
      * identify a set of variables X that will make the ignorability assumption hold
         * if we do this then the set of variables is sufficient to control for confounding 
      * using statistical methods to control for those variables and estimate causal effects
* Causal graphs: helpful for identifying which variables to control for
   * DAGs: No undirected paths, No cycles
* Relationship between DAGs and probability distributions
   * a DAG will tell us:
      * which variables are independent from each other
      * which variables are conditionally independent from each other
      * i.e. ways that we can factor and simplify the joint distribution 
   *  ![Screen Shot 2024-06-04 at 10 19 31 AM](https://github.com/jinfeijoy/causality/assets/16402963/abca2659-c862-4620-873f-e92cfd8bb096)
   *  ![Screen Shot 2024-06-04 at 10 21 34 AM](https://github.com/jinfeijoy/causality/assets/16402963/abd8d544-a074-49d7-a012-33b0bebb47a5)
   *  ![Screen Shot 2024-06-04 at 10 23 18 AM](https://github.com/jinfeijoy/causality/assets/16402963/2c8cdfdd-6150-4e84-9a12-5a4b4f1f805b)
   *  ![Screen Shot 2024-06-04 at 10 25 11 AM](https://github.com/jinfeijoy/causality/assets/16402963/a123fde5-5114-44b4-9f7e-26dc004f23a9)
   *  ![Screen Shot 2024-06-04 at 10 25 59 AM](https://github.com/jinfeijoy/causality/assets/16402963/4976c398-81de-42f5-99a6-e286b1576ff3)
   *  ![Screen Shot 2024-06-04 at 10 27 09 AM](https://github.com/jinfeijoy/causality/assets/16402963/a770217c-5ac1-4c10-99c9-51dde3cca1b1)
* Path and associations
   * types of paths
       * Forks: D<-E->F
       * Chains: D->E->F
       * Inverted forks: D->E<-F 
   *  Associations:
       * if nodes A and B are on the ends of a path, they are associated if
          * some information flows to both of them (forks)
          * information from one makes it to the other (chains)
       * inverted forks: not association
          * information from A and B collide at G: A->G<-B
          * G is known as collider
          * A and B both affect G:
            * information does not flow from G either A or B
            * So A and B independent (if this was the only path between them)        
* Conditional independent (d-seperation)
   * Blocking
      * consider the path A->G->B, if we condition on G, we block the path from A to B.
      * Suppose temperature (A) affects whether or not sidewalks are icy (G), which affects whether or not someone falls (B): A->G->B. However, if we restrict to situations where sidewalks are icy (condition on G) then temperature and falling are not associated via this path.
      * associations on a fork can also be blcoked: considering the path A<-G->B, if we condition on G, this path from A to B is blocked.
      * consider the path: A->G<-B, here A and B are not associated via this path (information collides at G), however, conditioning on G include an association between A and B.  
   *  Conditioning on collider
      * suppose:
         * A is the state of an on/off switch
         * B is the state of a different on/off switch
         * G is whether the lightbulb is lit up
         * A is determined from a coin flip, B is determined from a separate, independent coin flip, G is lit up only if both A and B are in the on state.
      * Then:
         * A and B are independent, if I tell you that b is on, it tells you nothing about A
         * A and B are dependent, given G, if I tell you that the light is off(G), then A must be off if B is on, and vice versa
   * D-seperation
      * Rules for d-seperation
         * a path is d-seperated by a set of nodes C if:
            * it contains a chain (D->E->F) and the middle part is in C OR
            * it contains a fork (D<-E->F) and the middle part is in C OR
            * it contains an inverted fork (D->E<-F) and the middle part is not in C, nor are any descendants of it
      * two nodes, A and B, are d-seperated by a set of nodes C if it blocks every path from A to B
         * then: A independent from B conditional on C
         * recall the ignorability assumption: Y0,Y1 independent from A conditional on X 
* Confounding revisited
   * frontdoor path: from A to Y is one that begins with an arrow emanating out of A
      *![Screen Shot 2024-06-04 at 11 48 19 AM](https://github.com/jinfeijoy/causality/assets/16402963/b2982e4b-d69f-420d-84be-18530e4fd44d)
      * we do not worry about front door paths, because they capture effects of treatment
      * we care about if we manipulate A, how is Y affected? , controling for Z would be controlling for an effect of treatment.
      * causal mediation analysis involves understanding frontdoor paths from A to Y
   * backdoor path: from treatment A to outcome Y are paths from A to Y that travel through arraows going into A:
      * ![Screen Shot 2024-06-04 at 11 48 46 AM](https://github.com/jinfeijoy/causality/assets/16402963/39a2b29d-1d70-4faa-ad9f-9202f87adb9d)
      * Here A<-X->Y is a backdoor path from A to Y
      * backdoor paths confound the relationship between A and Y, those need to be blocked.
      * to sufficiently control for confounding, must identify a set of variables that block all backdoor paths from treatment to outcome.
      * if X is this set of variables, then: Y0, Y1 independent A given X
* Backdoor path criterion: to use for variable selection for controlling
   * sufficient sets of confounders:
      * it blocks all backdoor paths from treatment to the outcome
      * it does not include any descendants of treatment
      * not necessary unique
      * ![Screen Shot 2024-06-04 at 11 58 58 AM](https://github.com/jinfeijoy/causality/assets/16402963/d147c1c9-0b34-4153-b830-07eec2b3bcc0)
      * ![Screen Shot 2024-06-04 at 12 00 12 PM](https://github.com/jinfeijoy/causality/assets/16402963/7b1bc246-1784-4dd5-a5f7-af2d86b83a53)
      * ![Screen Shot 2024-06-04 at 12 01 16 PM](https://github.com/jinfeijoy/causality/assets/16402963/5084f3be-2890-48bd-a5e6-f5f1b99b0f94)
* Disjunctive cause criterion

## Week3   
* Observational studies
   *  Randomized Trail
      * given X is sufficient to control for confounding: <img width="206" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/1b62e2d2-3538-432f-81f5-92cfbf48dc76">
      * in a randomized trail, treatment assignment A would be determined by a coin toss - effectively erasing the arrow from X to A: <img width="249" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/548d2654-f39c-4ae4-80f3-cf03bcbf7a4c">, no backdoor paath from A to Y
      * in randomized trail: the distribution of X will be the same in both treatment groups, thus, if the outcome distribution ends up differing, it will not be because of differences in X 
   * Observational studies
      *  planned,  prospective, observational studies with active data collection
         * like trails: data collected on a common set of variables at planned times; outcomes carefully measured, study protocols
         * unlike trails: regulations much weaker, since not intervening; broader population eligible for the study
     * Dtabases, retrospective, passive data collection
        * e.g. electronic medical records; claims; registries
        * large sample size; inexpensive; potential for rapid analysis
        * data quality typically lower; no uniform standard of collection 
   * in observational studies, the distribution of X will differ from treatment groups, for example, if older people are more likely to get A=1.
   * Matching: is a method that attempts to make an observational study more like a randomized trail: match individuals in the treated group (A=1) to individuals in the control group (A=0) on the covariates X.
      * once data are matched, essentially treated as if from a randomized trail 
* Mathcing
   * target population: we are making the distribution of covariates in the control population look like that in the treated population
   * Mahalanobis distance: <img width="469" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/9b83d285-6791-4eb5-9da0-038313adb4c9">,  where S = cov(X)
   * robust mahalanobis distance: can deal with outliers properly by:
      * replace each covariate value with its rank
      * constand diagonal on covariance matrix
      * calculate the usual mahalanobis distance on the ranks 
   * greedy (nearest neighbor) matching: not as good, but computationally fast (not globally optimal)
      *  Steps
         *  randomly order your list of treated subject and control subjects
         *  start with the first treated subject, match to the control with the smallest distance
         *  remove the matched control from the list of available matches
         *  move on to the next treated subject, match to the control with the smallest diatnce
         *  repeat step 3 and 4 until you have matched all treated subjects
      *  R package: Matchlt
      *  tradeoffs:
         *  pair matching
            * closer matches / faster computing time  
         *  many-to-one
            * larger sample size  
         *  largely a bias-variance tradeoff issue
      * Caliper: maximum acceptable distance 
   * optimal matching: better, but computationally demanding
      *  minimize global distance measure
      *  computationally demanding
      *  R package: optmatch / rcbalance
  * Assessing balance: how to check whether matching seemed to work
     * hypothesis test and p-value: two sample t-test / report p-value for each test, drawback: p-value are dependent on sample size, small difference in means will have a small p-value if the sample size is large
     * covariate balance - standardized difference: <img width="517" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/b7675d18-48a8-4b19-9ad0-5153834c22ef">
        * does not depend on sample size
        * often, absolute value of smd is reported
        * calculate for each variable that you match on
        * rules of thumb: value < 0.1 indicate adequate balance / value between 0.1-0.2 are not too alarming / value > 0.2 indicate serious imbalance
        * example: <img width="744" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/8f2a2918-8995-41c7-be6b-c1d5dd969b25">
  * Analyzing data after matching
     *  test for a treatment test
        * randomization test (permutation test / exact test)
           * compute test statistic from observed data
           * assume null hypothesis of no treatment effect is true
           * randomly permute treatment assignment within pairs and recompute test statistics (switch treated result with control result)
           * repeat many times and see how unusual observed statistic is
           * this test is equivalent to McNemar test for paired data :<img width="707" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/3bb850b0-052d-4eb9-ac15-3713a94c6790">
           * could also use a paired t-test for continuous data: <img width="698" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/5129445f-00fe-4adb-90cb-6a9c3f44827b">
     *  estimate a treatment effect and confidence interval
     *  methods should take matching into account
     *  Other outcome models:
        * conditional logistic regression : matched binary outcome data
        * stratified cox model
           * time-to-event (survival) outcome data
           * baseline hazard stratified on matched sets 
        * generalized estimating equiations (GEE)
           * Match ID variable used to specify cluster
           * for binary outcomes, can estimate a causal risk difference, causal risk ratio, or causal odds ratio (depending on link function)
  * sensitivity analysis
     * possible hidden bias
        * matching aims to achieve balance on observed covariates: overt bias could occur if there was imbalance on observed covariates
        * there is no guarantee that matching will result in balance on variable that we didn't match on: hidden bias: if these unobserved variables are confounders  
     * main idea: if there is hidden bias, determine how severe it would have to be to change conclusions
        * change from statistically significant to not (if there is hidden bias, how severe would it have to be before conclusions changed)
        * change in direction of effect (how much bias would there have to be before design actually changed so where we would have a different direction of the treatment effect.)
     * <img width="746" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/561c5b3d-bc14-4ae8-87cc-6bce3940db4e">
     * suppose we have evidence of a treatment effect: this is under the assumption that Gamma = 1, assume no hidden bias
     * we can then increase Gamma until evidence of treatment effect goes away (no longer statistically significant), once Gamma close to 1, sensitive to unmeasured confounding (hidden bias), if Gamma >> 1, not sensitive to unmeasured confounding
     * R package: sensitivity2x2xk, sensitivityfull
  * [R Code](https://www.coursera.org/learn/crash-course-in-causality/lecture/TZ01D/data-example-in-r)
* Propensity Score
  * Propensity score: the probability of receiving treatment, rather than control, given covariates X, define A=1 for treatment and A=0 for control, propensity score PI = P(A=1|X) (i.e. P(A=1|age=60)>P(A=1|age=30))
  * balancing score: 2 subjects have same propensity score, but they possibly have different covariate values X
     * despite the different covariate values, they were both equally likely to have been treated.
        * this means that both subjects X is just as likely to be found in the treatment group
        * if you restrict to a subpopulation of subjects who have the same value of the propensity score, there should be balance in the two treatment groups
        * the propensity score is a balancing score
     * P(X=x|PI(X)=p, A=1) = P(X=x|PI(X)=p, A=0)
     * IF WE MATCH ON THE PROPENSITY SCORE, WE SHOULD ACHIEVE BALANCE
     * conditioning on propensity score,  is conditioning on an allocation probability
  * estimated propensity score
     * in randomized trail, the propensity score is generally known (e.g. P(A=1|X)=P(A=1)=0.5
     * In observational study, it will be unknown
     * we need to estimate P(A=1|X)
        * the outcome here is A, which is binary
        * we therefore could estimate the propensity score using logistic regression
          * fit a logistic regression model: outcome A, covariate X
          * from that mode, get the predicted probability for each subject  
  * Propensity score matching
     * Overlap: once propensity score is estimated, it's usful to look for overlap: compare the distribution of the propensity score for treated and control subjects
        * <img width="853" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/f2454c97-4a05-44d9-84e8-bad904452b35">
        * <img width="866" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/72ce0fb9-7372-43f9-9e04-8271360e626a">
        * jitter plot <img width="584" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/aaee5d34-c0fc-4337-8ba7-849759aaae65">
     * trimming tails:
        * if there is a lack of overlap, trimming the tails is an option
           * this means removing subjects who have extrame values of the propensity score
              * removing:
                 * control subjects whose propensity score is less than the minimum in the treatment group
                 * treated subjects whose propensity score is greater than the maximum in the control group  
     * Matching
        * we can proceed by computing a distance between the propensity score for each treated subject with every control
        * in practice, logit (log-odds) of the propensity score is often used, rather than the propensity score itself
           * the propensity score is bounded between 0 and 1, making many values seems similar
           * logit of the propensity score is unbounded - this transformation essentially stretches the distribution, while preserving ranks
           * match on logit(PI) rather than PI   
     * Caliper
        * to ensure that we do not accept any bad matches, a caliper can be used, caliper is the maximum distance that we are willing to tolerate
        * in practice, a common choice for a caliper is the 0.2 times the standard deviation of logit of the propensity score
           * estimate the propensity score
           * logit-transform the propensity score
           * take the standard deviation of this transformed variable
           * set the caliper to 0.2 times the value from previous step
           * smaller caliper - less bias, more variable 
     * After matching
        * the outcome analysis methods can be the same as would be used if matching directly on covariates
           * randomization tests
           * conditional logistic regression, GEE, stratified cox model
           * jitter plot
     * [R Code](https://www.coursera.org/learn/crash-course-in-causality/lecture/VtFdu/propensity-score-matching-in-r)

## Week4 Inverse Probability of Treatment Weighting (IPTW)
* [Notes by T Yun](https://tyun.io/p/causal-inference-course-note1/)

## Week5 Instrumental Variables Methods
* Instrumental Variables Introduction
   * suppose there are unmeasured/obonbserved variables, U that affect A and Y. Then we have unmeasured confounding. <img width="159" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/42d2d270-0a29-4ea9-8cb3-002a1f671383">
   * If there is unmeasured confounding, cannot marginalize over all confounders (via matching, IPTW, etc)
   * IV method does not focus on the average causal effect for the population, they focus on a **local average treatment effect**
   * instrument variables (IV) is an alternative causal inference method that does not rely on the ignorrability assumption.
      * it affect treatment, but does not directly affect the outcome
      * think of Z as encouragement: <img width="288" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/2cc47338-0308-402a-9562-1c15c7a2d5cc">
      *  an intention-to-treat analysis would focus on the causal effect of encouragement
* Randomized trails with noncompliance
   * Setup
      * Z: randomization to treatment
      * A: treatment received
      * Y: outcome
      * Note: typically, not everyone assigned treatment will actually receive the treatment (non-compliance)
  * DAG
      * Non-compliance makes a randomized trail like an observational study
      * there could be confounding based on treatment received
      *  <img width="294" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/a57a4888-b400-4542-ab6b-9876fbae9c68">
  *  Causal effect of assignment on receipt
      * we can think of the average causal effect of treatment assignment on treatment received as  E(A1-A0)
      * This is generally estimable from the observed data, by randomization and consistency: E(A1) = E(A|Z=1), E(A0) = E(A|Z=0)  
      * we can think of the average causal effect of treatment assignment on outcome as  E(Y1-Y0)
* Compliance Classes
   * potential value of treatment: <img width="620" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/0f2934a5-be6d-4360-8214-8e2ce064cba5">
      * never takers: do not take treatment, regardless of randomization: encouragement does not work; we would not learn anything about the efect of treatment in this subpopulation, as there is no variation in treatment received
      * **compliers**: take treatment when encouraged to, and do not otherwies. in this group, treatment received is randomized
      * defiers: do the opposite of what they are encouraged to do, in this group treatment received is also randomized, but in the opposite way
      * always-takers: always take treatment, in this group there is no variation in treatment received. no information about causal effect 
      * 
   * local average treatment effect
      * the target of inference is: <img width="615" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/2263cb73-3029-4da5-95dc-d1181fdc0565">
      * known as complier average causal effect (CACE)
         * this is a causal effect in a subpopulation
         * a local causal effect
         * no inference about defiers, always-takers, or never-takers
   * Observed data
      * <img width="884" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/c48df328-16b9-4873-a444-195f33324349">
      * challange: without additional assumption, we cannot classify each subject into one of these categories, we can narrow it down to two options, however
* Assumptions
   * Assumptions about IVs: a variable is an IV if:
      * it is associate with the treatment
      * it affects the outcome only through its effect on treatment (cannot directly or indirectly through its effect on U, affect the outcome), this is known as exclusion restriction
         * <img width="512" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/05a8c060-21d2-474a-b592-1a4c4787c78c">
         * <img width="387" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/fbd43dbb-1b16-42b1-ba81-4728615dddec">
   * Monotonicity assumption: there are no deliers
      * no one consistently does the opposite of what they are told
      * it is called monotonicity because the assumption is that the probability of treatment should increase with more encouragement
      * <img width="878" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/e683791f-949f-4ec5-8826-10b98035318a">
* Causal effect identification and estimation
   * Identification of causal effects
      * <img width="522" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/26dcf889-9ae2-483a-91af-4bd804afaa29">
      * <img width="674" alt="image" src="https://github.com/jinfeijoy/causality/assets/16402963/e3f5878b-f162-4cc9-8663-9484a5fd639f">: among always takers and never takers, Z does nothing
      * ![image](https://github.com/jinfeijoy/causality/assets/16402963/66772777-b166-424a-9b81-4893aad8385c)
      * ![image](https://github.com/jinfeijoy/causality/assets/16402963/71fd8f0e-d638-4121-a258-0e8846a8042f)
      * ![image](https://github.com/jinfeijoy/causality/assets/16402963/692e530c-f5d3-4b71-8667-1723f684912a)
* IVs in observational studies
   *  Examples
      *  ![image](https://github.com/jinfeijoy/causality/assets/16402963/17144700-4348-45fc-a4c1-2fba48ae4e71), exclusion restriction: calendar time could be associated with the outcome if other treatment practices or patient behaviours changed during that time 
      *  ![image](https://github.com/jinfeijoy/causality/assets/16402963/b7b7a2ea-c937-48b1-8001-e8d141f339f1)
      *  ![image](https://github.com/jinfeijoy/causality/assets/16402963/a46260f3-5df0-4518-a9d6-d174b58dae36)
* Two stage least squares
   *  stage 1: ![image](https://github.com/jinfeijoy/causality/assets/16402963/9565de54-3cba-4771-a285-67899a95a69a)
   *  stage 2: ![image](https://github.com/jinfeijoy/causality/assets/16402963/f4bbfb46-6b61-40d0-a380-c8ba69f2be36)
   *  2SLS Estimator:
      *  ![image](https://github.com/jinfeijoy/causality/assets/16402963/8e8cf79a-dab9-4bd9-9db0-acb74de090eb)
      *  ![image](https://github.com/jinfeijoy/causality/assets/16402963/c7089d37-ab63-4aee-8413-6a88c109baf6)
      *  ![image](https://github.com/jinfeijoy/causality/assets/16402963/33fb5658-4591-497e-b55e-a43c2342b54e)
   * sensitivity analysis
      * ![image](https://github.com/jinfeijoy/causality/assets/16402963/3f1d550b-1c87-4371-b3d3-a5bedccea26c)
* Weak instruments
   * strength of IVs: we can measure the strength of an instrument by estimate the proportion of compliers, estimate: E(A|Z=1)-E(A|Z=0)
   * A weak instrument causes problems: suppose only 1% of the population are compliers, if the sample size of our data set is n, then only 1% of n have useful information about treatment. this leads to very large variance estimates, estimate of causal effect unstable.
   * if the IV is weak, an IV analysis might not be the best option, it would likely produce confidence intervals that are too wide to be useful. 
* [IV analysis in R](https://www.coursera.org/learn/crash-course-in-causality/lecture/D19Ae/iv-analysis-in-r)
   * R package: ivpack 
