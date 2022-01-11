
# Graph Neural Network Cancer Drug Response (gnnCDR)

A major goal in precision oncology is to match a patient and tumor to the optimal therapeutic treatment. Research towards these goals include identifying drug combinations or repurposing drugs used in other domains to address limitations in oncology treatment durability, drug resistance and patient toxicity. We seek to accelerate and improve drug development by developing algorithms that improve how we identify therapeutic drug combinations based on ‘omic features and improve predictions of drug response.

## Project Summary 

Ineffective or limited precision oncology treatments are a cause of patient mortality. We seek to address this challenge by improving pre-clinical drug repurposing and drug combination discovery. We highlight the methodological challenge of training drug response models using single-drug data that will generalize well to multi-drug perturbations. We operate on the premise that protein-protein interactions mediate cellular drug response and hypothesize that incorporating this prior knowledge in a deep learning framework is liable to overcome limitations in drug response modeling and enable novel approaches to drug prioritization. To do this we will predict drug perturbed mRNA expression from intrinsic cancer features using graph neural networks that operate on literature curated protein-protein and drug-target interactions. In preliminary research, we have developed a synthetic data generator, which we have used to show promise and feasibility of our approach. We will develop and evaluate our methods using synthetic data before applying it to cancer cell line drug-perturbed mRNA expression datasets to prioritize drug combinations. Therapeutic candidates will be empirically evaluated in Dr. Gordon Mills’ and Dr. Jeffrey Tyner’s labs. Successful implementation of our methods will enable tractable and robust drug prioritization based on nuanced therapeutic goals such as user-defined cell type selective response. 

# Installation 

...