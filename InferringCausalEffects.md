# Inferring Causal Effects

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
  * sensitivity analysis
* 
