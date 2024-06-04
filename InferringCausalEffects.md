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



  
   
* 
