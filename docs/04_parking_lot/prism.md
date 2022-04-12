# Goal: Train a model to predict cell viabilty (~PRISM surrogate) using perturbed expression latent state (GNNCDR time-agnostic latent state). 

## Exog. 

Use a pre-trained GNNCDR model to predict perturbed expression time-agnostic latent state (z in GNNCDR model figures). 

## Endog. 
Use PRISM assay, as provided by depmap. This comes in two flavors ... 

Primary Screen: All 1 dose (2.5 uM) ~ lots of drugs 
Secondary Screen: 8 Dose points ~ fewer drugs 

outcome is provided in form of logfold change compared to DMSO controls... e.g., outcome = abundance_drug / abundance_dmso 
then:   

- outcome > 1 ~ stimulates growth 
- outcome = 1 ~ no difference in behavior 
- outcome < 1 ~ inhibitory 

General range of data in [primary screen](https://depmap.org/portal/download/all/?releasename=PRISM+Repurposing+19Q4&filename=primary-screen-replicate-collapsed-logfold-change.csv) ~ [-5,2]

From the secondary screen [readme](https://depmap.org/portal/download/all/?releasename=PRISM+Repurposing+19Q4&filename=secondary-readme.txt), they claim to calculate `cell viability` using: 

>> **"Calculate viability data as two to the power of replicate-level logfold change data."** 

However, that would lead to values between 0-2 (assuming not stimulatory behavior). I assume they mean they use: 

$$ cell\_viability = 2^{(logfold\_change - 1)} $$

Which will result in values [0,1] being inhibitory, >1 being stimulatory. 

## Questions: 
- How many drugs overlap with those used in GNNCDR? 
- How many cell lines overlap with those used in GNNCDR? 
    - in primary screen? in secondary screen? 


References: 

>> 1. Corsello SM, Nagari RT, Spangler RD, Rossen J, Kocak M, Bryan JG, Humeidi R, Peck D, Wu X, Tang AA, Wang VM, Bender SA, Lemire E, Narayan R, Montgomery P, Ben-David U, Garvie CW, Chen Y, Rees MG, Lyons NJ, McFarland JM, Wong BT, Wang L, Dumont N, O'Hearn PJ, Stefan E, Doench JG, Harrington CN, Greulich H, Meyerson M, Vazquez F, Subramanian A, Roth JA, Bittker JA, Boehm JS, Mader CC, Tsherniak A, Golub TR. Discovering the anti-cancer potential of non-oncology drugs by systematic viability profiling. Nat Cancer. 2020 Feb;1(2):235-248. doi: 10.1038/s43018-019-0018-6. Epub 2020 Jan 20. PMID: 32613204; PMCID: PMC7328899.