# ORKG Astronomy NER
## Overview

### Aims

The ORKG Astro-NER system automatically extracts contribution-centric scholarly entities from the titles of astronomy literature.  The twelve entities are drawn from the definitions in previous works on astronomy NER ([Becker et al., 2005](https://www.researchgate.net/publication/258512818_Optimising_Selective_Sampling_for_Bootstrapping_Named_Entity_Recognition); [Murphy et al., 2006](https://aclanthology.org/U06-1010/); [Grezes et al., 2022](https://aclanthology.org/2022.wiesp-1.1/)), contribution-centric NER ([D’Souza and Auer, 2022](https://link.springer.com/chapter/10.1007/978-3-031-21756-2_3); [D’Souza, 2023](https://www.preprints.org/manuscript/202305.1393/v1)), and the top-level concepts in the Ontology of Astronomical Object Types ([Derriere et al., 2010](https://www.ivoa.net/documents/Notes/AstrObjectOntology/)), and then adapted to our specific task.  The twelve entity types are shown in the table below.



| **Entity** |                                       **Definition**                                        |
|:--------:|:-----------------------------------------------------------------------------------------:|
|  AstrObject   | All concepts representing astronomical objects, e.g. black holes.|
|  AstroPortion   | All concepts representing portions of astronomical objects which are not astronomical objects themselves, e.g. sunspots.|
|  ChemicalSpecies   | Atomic elements such as element names from the periodic table, atoms, nuclei, dark matter, e.g. Fe.|
|  Instrument   | Names of measurement instruments, including  telescopes, e.g. Large Hadron Collider.|
|  Measurement   | Measured observational parameters or properties (both property and value), e.g. frequency.|
|  Method   | Abstractions which are commonly used to support the solution of the investigation, e.g. minimal supersymmetrical model.|
|  Morphology   | Geometry or morphology of astronomical objects or physical phenomena, e.g. asymmetrical.|
|  PhysicalQuantity   | Properties of physical phenomena interacting, e.g. gravity.|
|  Process   | Phenomenon or associated process, e.g. Higgs boson decay.|
|  Project   | Survey or research mission, e.g. the dark energy survey.|
|  ResearchProblem   | The theme of the investigation, e.g. final state hadronic interactions.|
|  SpectralRegime   | Observed or analyzed electromagnetic spectrum, e.g. mega electron volt.|

### Approach
Based on the annotated dataset (findable under [`/data/processed`](data/processed)) we fine-tune four different models using the [HuggingFace architecture](https://huggingface.co/docs/transformers/index) and define a token classification task.

The models are:
* FLAN-T5 ([Chung et al., 2022](https://arxiv.org/abs/2210.11416)) in the Small (77M) and Base (247M) sizes
* mT5 ([Xue et al., 2021](https://aclanthology.org/2021.naacl-main.41/)) in the Small (300M) and Base (582M) sizes

### Dataset

Our data source consists of the titles from around 15,000 astronomy articles with the CC-BY redistributable license, downloaded from Elsevier.  From this, approximately 5000 titles were randomly selected for annotation by two graduate students.

* [`/data/processed`](data/processed): the complete annotated dataset 
* [`/data/experimental`](data/experimental): the same 1500 titles with human annotations and predictions from GPT-3.5, GPT-3.5 with finetuning, and GPT-4.0
* [`/data/IAA`](data/IAA): the files used to calculate inter-annotator agreement
    * [`/data/IAA/Phase_I`](data/IAA/Phase_I): 100 titles labeled by both annotators
    * [`/data/IAA/Phase_II`](data/IAA/Phase_II): 100 titles labeled by both annotators and a domain expert

## How to run

### Prerequisites

#### Software Dependencies
* Python version ``^3.7.1``

#### Hardware Resources
* RAM ``~12 GB``
* Storage ``78 GB`` 
* Processor ``CPU``

### Cloning the repository

```commandline
git clone https://gitlab.com/TIBHannover/orkg/nlp/experiments/orkg-astronomy-ner.git
cd orkg-astronomy-ner
pip install -r requirements.txt
```


## Contribution
This service is developed and maintained by:
* D'Souza, Jennifer <jennifer.dsouza@tib.eu>
* Evans, Julia <julia.evans@tib.eu>

## License
[MIT](./LICENSE)


## References

* Hyung Won Chung, Le Hou, Shayne Longpre, Barret Zoph, Yi Tay, William Fedus, Yunxuan Li, Xuezhi Wang, Mostafa Dehghani, Siddhartha Brahma, Albert Webson, Shixiang Shane Gu, Zhuyun Dai, Mirac Suzgun, Xinyun Chen, Aakanksha Chowdhery, Alex Castro-Ros, Marie Pellat, Kevin Robinson, Dasha Valter, Sharan Narang, Gaurav Mishra, Adams Yu, Vincent Zhao, Yanping Huang, Andrew Dai, Hongkun Yu, Slav Petrov, Ed H. Chi, Jeff Dean, Jacob Devlin, Adam Roberts, Denny Zhou, Quoc V. Le, and Jason Wei. 2022. "[Scaling Instruction-Finetuned Language Models.](https://arxiv.org/abs/2210.11416)"
* Markus Becker, Benjamin Hachey, Beatrice Alex, and Claire Grover. 2005. "[Optimising Selective Sampling for Bootstrapping Named Entity Recognition.](https://www.researchgate.net/publication/258512818_Optimising_Selective_Sampling_for_Bootstrapping_Named_Entity_Recognition)" In Proceedings of the ICML-2005 Workshop on Learning with Multiple Views, Bonn, Germany.
* Sébastien Derriere, Andrea Preite-Martinez, Alexandre Richard, Laurent Cambrésy, and Paolo Padovani. 2010. "[Ontology of Astronomical Object Types](https://www.ivoa.net/documents/Notes/AstrObjectOntology/)" Version 1.3. International Virtual Observatory Alliance.
* Jennifer D’Souza and Sören Auer. 2022. "[Computer Science Named Entity Recognition in the Open Research Knowledge Graph.](https://link.springer.com/chapter/10.1007/978-3-031-21756-2_3)" In From Born-Physical to Born-Virtual: Augmenting Intelligence in Digital Libraries, pages 35–45, Hanoi, Vietnam. Springer International Publishing.
* Jennifer D’Souza. 2023. "[Agriculture Named Entity Recognition - Towards FAIR, Reusable Scholarly Contributions in Agriculture.](https://www.preprints.org/manuscript/202305.1393/v1)" Preprint.
* Felix Grezes, Sergi Blanco-Cuaresma, Thomas Allen, and Tirthankar Ghosal. 2022. "[Overview of the First Shared Task on Detecting Entities in the Astrophysics Literature (DEAL).](https://aclanthology.org/2022.wiesp-1.1/)" In Proceedings of the first Workshop on Information Extraction from Scientific Publications, pages 1–7, Online. Association for Computational Linguistics.
* Tara Murphy, Tara McIntosh, and James R. Curran. 2006. "[Named Entity Recognition for Astronomy Literature.](https://aclanthology.org/U06-1010/)" In Proceedings of the Australasian Language Technology Workshop 2006, pages 59–66, Sydney, Australia.
* Linting Xue, Noah Constant, Adam Roberts, Mihir Kale, Rami Al-Rfou, Aditya Siddhant, Aditya Barua, and Colin Raffel. 2021. "[mT5: A Massively Multilingual Pre-trained Text-to-Text Transformer.](https://aclanthology.org/2021.naacl-main.41/)" In Proceedings of the 2021 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, pages 483–498, Online. Association for Computational Linguistics.


