# The Synthetic `gnnCDR` data object 

Now that we've generated synthetic data, we need to organize it in a format conducive to `graph neural networks`. We will use [`pytorch_geometric`](https://pytorch-geometric.readthedocs.io/en/latest/index.html) to build our deep learning models, and therefore need to create a [`HeteroData`](https://pytorch-geometric.readthedocs.io/en/latest/notes/heterogeneous.html) object that holds a single observation. 

We will format our synthetic data as a heterogenous graph with 6 node types: 

- protein
- agonist
- inhibitor
- KO (knockout)
- KD (knockdown) 
- OE (overexpression)

The genetic nodes do not have any node attributes and only target a single protein. The chemical perturbations have concentration node attributes (`conc`) and can target multiple protein nodes. Protein-protein edges can be of two types: "activate" and "inhibit". This is illustrated in figure 1 below. 

![](./synth_data_graph_obj.PNG)
**Figure 1**: Graphic of our HeteroData object. 

> **Note**: To keep the graph as small as possible, each data observation only includes perturbation edge indices from `active/present` pertubation nodes, e.g., For an observation given perturbation `G01_KO` (KO of protein G01) then the `data['KO','targets','protein'].edge_index` will only include edges that go from `G01_KO` to proteins and all other perturbation nodes will be excluded. 

This process keeps the graph small, which we believe will speed up training and inference. Since `genetic perturbations` don't have node attributes, it is the *presence* of the node that creates the perturbation. Chemical perturbations operate differently as they have a `concentration` node attribute and we assume that a concentration value of 0 will behave identically to that node being removed from the graph entirely. 

# `HeteroSynthDataset` Object

We extend the pytorch_geometric Dataset object and create a `HeteroSynthDataset` which functions to parse the synthetic `hdf5` file and produce individual observations of the form described above. 

As described above, only active perturbation nodes are included in each observation - but the perturbation indexing remains the same across all observations. 

A dataset object can be initialized by: 

```python 

dataset = SynthHeteroDataset('../../data/synthetic_data.h5', 
                             indices=None, 
                             zscore=False, 
                             x_noise=None, 
                             y_noise=None, 
                             x_sparsity=None, 
                             y_sparsity=None, 
                             ppi_false=None, 
                             dti_false=None, 
                             ppi_missing=None, 
                             dti_missing=None, 
                             seed=None)

```

Passing an array of integers to `indices` (indexed by the `synthetic_data.h5`) will specfy what data will be included in the dataset. This can be used to specify train/test splits or filter observations. 

Here are two examples of a returned data object. 

> perturbation: `agonist_2`

```bash

HeteroData(
  line=[1],
  context=[1, 10],
  time=[1],
  pert_all=[1, 88],
  pert_name=[1],
  conc=[1],
  pert_type=[1],
  protein={
    x=[1, 100],
    y=[1, 100]
  },
  agonist={ conc=[5] },
  (protein, activates, protein)={ edge_index=[2, 66] },
  (protein, inhibits, protein)={ edge_index=[2, 59] },
  (agonist, targets, protein)={ edge_index=[2, 2] }
)
```

> perturbation: `None` ("WT")

```bash

HeteroData(
  line=[1],
  context=[1, 10],
  time=[1],
  pert_all=[1, 88],
  pert_name=[1],
  conc=[1],
  pert_type=[1],
  protein={
    x=[1, 100],
    y=[1, 100]
  },
  (protein, activates, protein)={ edge_index=[2, 66] },
  (protein, inhibits, protein)={ edge_index=[2, 59] }
) 

```
Note that the 'WT' perturbation does not have any edges from perturbation nodes to protein nodes wheras the `agonist_2` observation has an `(agonist, targets, protein) edge index`. Also note, there are only 2 edges in the agonist `edge_index`. If you were to inspect the edge_index, it would only have values from `agonist_2` to a protein, e.g., all perturbation edges from other *inactive* perturbations have been filtered. 