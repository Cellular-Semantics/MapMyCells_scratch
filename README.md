# MapMyCellsScratch

## Input

Collection: [Phenotypic variation of transcriptomic cell types in mouse motor cortex
](https://cellxgene.cziscience.com/collections/20a1dadf-a3a7-4783-b311-fcff3c457763)
= Scala et al., 2021 https://www.nature.com/articles/s41586-020-2907-3

Dataset: [All cells with electrophysiological recordings](https://cellxgene.cziscience.com/e/bf6a5c78-5a2e-4e34-93f3-7be5d127d879.cxg)

Species: Mouse 
### Cell type annotations:
 Cell_type:  {'GABAergic neuron', 'glutamatergic neuron', 'native cell'} 
 BICCN_cluster_label: {'L2/3 IT_2', 'L2/3 IT_3', 'L4/5 IT_1' ... }

## [MapMyCells](https://knowledge.brain-map.org/mapmycells/process/)

Mapped input h5ad against whole mouse brain using hierarchical mapping option.

i.e. the reference taxononmy for this mapping is CCN20230722 https://github.com/Cellular-Semantics/whole_mouse_brain_taxonomy 

=> output JSON file and csv file


 ### Output

Each individual cell has 3 mappings, class, subclass and clus.

In order to map thse map

```JSON
    {
      "CCN20230722_CLAS": {
        "assignment": "CS20230722_CLAS_01",
        "bootstrapping_probability": 1.0,
        "avg_correlation": 0.7759754574470855,
        "runner_up_assignment": [],
        "runner_up_correlation": [],
        "runner_up_probability": []
      },
      "CCN20230722_SUBC": {
        "assignment": "CS20230722_SUBC_004",
        "bootstrapping_probability": 1.0,
        "avg_correlation": 0.7060080230869373,
        "runner_up_assignment": [],
        "runner_up_correlation": [],
        "runner_up_probability": []
      },
      "CCN20230722_CLUS": {
        "assignment": "CS20230722_CLUS_0054",
        "bootstrapping_probability": 1.0,
        "avg_correlation": 0.6388730675117144,
        "runner_up_assignment": [],
        "runner_up_correlation": [],
        "runner_up_probability": []
      },
      "cell_id": "20171207_sample_7"
    }
```

csv has 

cell_id | class_label | class_name | class_bootstrapping_probability | subclass_label | subclass_name | subclass_bootstrapping_probability | cluster_label | cluster_name | cluster_alias | cluster_bootstrapping_probability
-- | -- | -- | -- | -- | -- | -- | -- | -- | -- | --
20171204_sample_2 | CS20230722_CLAS_01 | 01 IT-ET Glut | 1 | CS20230722_SUBC_022 | 022 L5 ET CTX Glut | 1 | CS20230722_CLUS_0364 | 0364 L5 ET CTX Glut_2 | 393 | 1 |  
20171204_sample_4 | CS20230722_CLAS_01 | 01 IT-ET Glut | 1 | CS20230722_SUBC_004 | 004 L6 IT CTX Glut | 1 | CS20230722_CLUS_0054 | 0054 L6 IT CTX Glut_5 | 110 | 1 |  


## Aim: Generate CAS from this input

This will be a separate CAS file from the original.  We will need an import mechanism to combine the two.

Spec by example: the cells 20171204_sample_2 and 20171204_sample_4 are both members of a new labelset

```yaml

labelsets:
 - 
   name: CS20230722_CLAS_01
   description: [MapMyCells](https://knowledge.brain-map.org/mapmycells/process/) Heierarchical Mapping run against whole mouse brain CS20230722.
   annotation_method: algorithmic 
   automated_annotation:
      algorithm_name: MapMyCells Hierarchical Mapping
      algorithm_version: # TBA if available
      algorithm_repo_url: # TBA - this is Nelson's work.  There is a repo available
      reference_location: https://knowledge.brain-map.org/data/LVDBJAW8BI5YSS1QUBG/summary

annotations:
   labelset: CS20230722_CLAS_01,
   cell_set_accession: CS20230722_CLAS_01,
   label: 01 IT-ET Glut
   cells:
      -
        cell_id: 20171204_sample_2
        confidence: 1
      -
        cell_id: 20171204_sample_4
        confidence: 1
```

What's missing above: We need a way to refer to the original taxonomy (where there is one).  This ideally would be via the full PURL.

CAS-Tools method will need additional args to get some of the more general labelset metadata as this is not available in the JSON.

Original labelsets for these cells for comparison

```yaml
   labelset: BICCN_cluster_label
   label: L5 IT_2
   cell_ids: 
      - 20171204_sample_4
      ...
```




