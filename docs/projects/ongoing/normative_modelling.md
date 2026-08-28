# Normative modelling (fMRI) project

## Project team

<div class="grid cards" markdown>

- ![](../../assets/profile_pictures/tim.jpg){ width="120" }  
  **Tim van Balkom**<sup>1</sup> 

- ![](../../assets/profile_pictures/chris.png){ width="120" }  
  **Chris Vriend**<sup>1</sup> 

- ![](../../assets/profile_pictures/odile.jpg){ width="120" }  
  **Odile van den Heuvel**<sup>1</sup> 

- ![](../../assets/profile_pictures/ysbrand.jpg){ width="120" }  
  **Ysbrand van der Werf**<sup>1</sup> 

- ![](../../assets/profile_pictures/andrew.jpeg){ width="120" }  
  **Andrew Zalesky**<sup>2</sup> 

- ![](../../assets/profile_pictures/sina.png){ width="120" }  
  **Sina Mansour L.**<sup>3</sup> 

</div>

---

<sup>1</sup>*Amsterdam UMC location Vrije Universiteit Amsterdam, Department of Anatomy and Neurosciences, Amsterdam, the Netherlands*

<sup>2</sup>*The University of Melbourne department of Biomedical Engineering and Psychiatry*

<sup>3</sup>*National University of Singapore Centre for Sleep and Cognition, The University of Melbourne department of Psychiatry* 

## Project summary

The aim of this study is to get a better understanding of the neuranatomical heterogeneity underlying cognitive impairment in PD using normative modelling. Given the involvement of various functional brain circuits in PD-related cognitive impairment that shows high interindividual variety, we aim to develop brain charts of "normal" functional connectivity across the aging lifespan. Using these brain charts, we can compute deviations from normal functional connectivity in a sample of individuals with PD and assess how interindividual variation in deviation from normal connectivity is related to cognitive heterogeneity.

In the future, we aim to use these models to inform treatment protocols that can modulate brain circuit function, e.g. repetitive transcranial magnetic stimulation. Moreover, detailed brain charts based on resting-state functional MRI have not yet been published and may prove highly valuable for other applications in neuropsychiatric disorders and neurological diseases.

Read more about this project in the full [secondary proposal PDF](../../assets/secondary_proposals/NormativeModelling_ENIGMA_Secondary_Proposal.pdf). 

Link to preregistration: *coming soon!*

Toolboxes used: [HALPpipe](https://github.com/HALFpipe/HALFpipe) for fMRI preprocessing; [SpectraNorm](https://sina-mansour.github.io/spectranorm/) and/or [PCNToolkit](https://pcntoolkit.readthedocs.io/en/latest/) for normative modelling.

## HALFpipe preprocessing pipeline

This study will apply preprocessing of resting-state fMRI using [HALPpipe](https://github.com/HALFpipe/HALFpipe). For the most part, we will apply the standard pipeline settings as outlined in the [HALFpipe documentation](https://fmri.science/halfpipe/new_ui.html).
- We will use [HALFpipe version 1.3.3.dev91+g892515660](https://surfdrive.surf.nl/s/ikDotZQx7YHJLdm). This version fixes important bugs from version 1.3.2 and before. **Please download the container via this link, not via the HALFpipe website (for version control)**
- For the general pipeline settings, including specifying data locations, whether or not BIDS-organized, and general preprocessing steps such as slice timing correction and initial volume removal, the [HALFpipe pipeline settings](https://fmri.science/halfpipe/new_ui.html#pipeline-settings) can be followed.
- For the atlas-based connectivity matrix, [the steps outlined in the HALFpipe manual can be followed](https://fmri.science/halfpipe/new_ui.html#atlas-based-connectivity-matrix). **Important note**: we will use two atlases: 1) HALFpipe standard [Schaefer 400P17N + aseg]() - "Schaefer2018Combined", and 2) [Schaefer 400P7N + Melbourne Subcortical Atlas S3]() - "Schaefer400P7NMSAS3". We will additionally use five pre-processing pipelines: 1) aCompCor, 2) Motion parameters with scrubbing, 3) Pipeline 2 + Global Signal (GSR), 4) Motion parameters, 5) Pipeline 4 + Global Signal (GSR).
- Quality assessment: **coming soon**
- Data sharing: **coming soon**


