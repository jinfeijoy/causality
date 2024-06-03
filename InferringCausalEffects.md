# Inferring Causal Effects

## Week1
* Confusion over Causality
  * ![causal1](https://github.com/jinfeijoy/causality/assets/16402963/ac59106b-ab90-4e5d-bcb9-6ab5c4c4f46b)
  * ![causal2](https://github.com/jinfeijoy/causality/assets/16402963/b57c02d7-ed81-4381-bc29-cfc72692e995)
* Causal Effect
  * ![c3](https://github.com/jinfeijoy/causality/assets/16402963/20c8ae26-3667-4989-81c9-af0edcfb2f64)
     * manupulated interventions are better defined and more actionable  
  * ![c4](https://github.com/jinfeijoy/causality/assets/16402963/d4bb1f1e-78a1-4e6d-9fff-6421a803ab4a)
     * hard to get result based on single treatment, so can use average to represent causal effect 
  * ![c5](https://github.com/jinfeijoy/causality/assets/16402963/687e5ee8-5da2-4061-b61e-391a55db15e0)
  * ![c6](https://github.com/jinfeijoy/causality/assets/16402963/1b4824d8-d0fb-4a1a-8e76-1cfa73a558f8)
  * ![c7](https://github.com/jinfeijoy/causality/assets/16402963/e7d3119f-8fd6-437a-a224-662af8458f2e)
* Causal Assumptions
   * Stable Unit Treatment Value Assumption (SUTVA)
      * ![IMG_2425](https://github.com/jinfeijoy/causality/assets/16402963/e89c1551-04c6-4a4a-b4fa-0db1b0dcedfe)
   * Consistency
      * ![IMG_2430](https://github.com/jinfeijoy/causality/assets/16402963/aa43013c-6fb4-42c1-a088-b6b99a9542dd)
   * Ignorability
      * ![IMG_2426](https://github.com/jinfeijoy/causality/assets/16402963/8744269a-de36-4d6f-bd4f-04f82ffed0f4)
      * ![IMG_2427](https://github.com/jinfeijoy/causality/assets/16402963/3e403513-4a40-4620-b78b-ce770ed02263)
   * Positivity
      * ![IMG_2431](https://github.com/jinfeijoy/causality/assets/16402963/b595581a-e281-495f-b6ed-18537247665e)
* Stratification
     * ![IMG_2428](https://github.com/jinfeijoy/causality/assets/16402963/19098a8b-d7f5-4e1d-a30b-5779bd81d391)
     * ![IMG_2429](https://github.com/jinfeijoy/causality/assets/16402963/78a2e014-aad8-4ed4-bd12-8fb1fa8e45d4)
*  Incident user and active comparator design
   * example as to estimate taking yoga's impact to blood presure, to design the event, taking snapshot will lose the information that people take yoga before centain period and then stop. in this case, we need to pick the data point that people initial yoga as first time, it's easy to find out cut-off time for active event, but it's hard to define time for non-active user (group of people not taking yoga class). In this case, we may need to find other active comparator, i.e. take zomba class. By doing so, the design will change and narrow.
   * ![Screen Shot 2024-06-03 at 1 39 14 PM](https://github.com/jinfeijoy/causality/assets/16402963/e859c254-2fde-4e58-ace3-f7128a4ba611)
  



  
   
* 
