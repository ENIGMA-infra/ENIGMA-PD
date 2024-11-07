# Welcome to the ENIGMA-PD FreeSurfer 7 guidelines!

This page is created to guide collaborating ENIGMA-PD sites through the FreeSurfer processing steps. The outcomes include cortical thickness, cortical surface area, and volume of subcortical regions and their subfields. All steps and code required are combined into the guidelines presented here. If you have any questions, concerns, or issues, please contact the ENIGMA-PD core team at enigma-pd@amsterdamumc.nl. 

## Leaderboard
To help motivate and monitor each site's progress, we maintain a leaderboard that outlines all the steps detailed in these guidelines. If you are in charge of data processing at your site, please request access and regularly update your progress on the current steps on the [ENIGMA-PD Leaderboard](https://docs.google.com/spreadsheets/d/13iGfh-97ZYnAyjT5egBDHmGhqXbsl1yo1A6QnPXQYbY/edit?usp=sharing).

## BIDSification
Before starting the analysis, organizing your data is essential — it will benefit this analysis and streamline any follow-up ENIGMA-PD work. We know it can be challenging, but we’re here to support you. 

For this analysis, please ensure T1-weighted images are organized according to the Brain Imaging Data Structure (BIDS) format. BIDS is a standardized format for organizing and labeling neuroimaging data to ensure consistency and make data easily shareable and analyzable across studies. Although we’re focusing on T1-weighted images for this analysis, organizing available diffusion-weighted or functional MRI data in BIDS will make future analyses easier.

Here are the core principles for organizing your neuroimaging data in BIDS format:
- Use consistent file and folder names
- Separate modalities
- Include metadata files
- Validate the structure

Resources from the BIDS community offer guidance on organizing your data, and BIDS converters can help automate this process, saving time and reducing manual errors. We recommend using Dcm2Bids (for DICOM's) and BIDScoin (for NIfTI's).
- [BIDS documentation](https://bids-website.readthedocs.io/en/latest/index.html)
- [Recommended converter; BIDScoin](https://bidscoin.readthedocs.io/en/stable/)
- [BIDS tutorials](https://www.youtube.com/watch?v=pAv9WuyyF3g&list=PLtJYlrqQ3YK_M4YgkUx6akJqlHF1R7A5g)

## Nipoppyfication
Nipoppy is a lightweight framework for standardized organization and processing of neuroimaging-clinical datasets. Its goal is to help users adopt the FAIR principles and improve the reproducibility of studies. Essentially an extension of BIDS, Nipoppy builds on the BIDS standard to enhance data organization, processing, and integration, further supporting standardized workflows and reproducible research practices.

The ongoing collaboration between the ENIGMA-PD team and Nipoppy developers has significantly improved dataset organization for the Amsterdam and open datasets. It has also streamlined the standardization of analysis workflows, made re-running pipelines for version updates easier, and simplified tracking of which datasets have been processed with specific analysis pipelines. The ENIGMA-PD and Nipoppy team is available to support and guide users through the process of implementing the framework, ensuring a smooth transition. Please get started at the [Nipoppy documentation](https://nipoppy.readthedocs.io/en/latest/index.html)

## Running FreeSurfer 7
The first step of running FS7 is to prepare your work environment with either Apptainer or Docker. We prefer Apptainer, but Docker can be used if you don't have admin rights or access to a Linux system.

### Installation
- [Install Apptainer](https://github.com/apptainer/apptainer/blob/main/INSTALL.md)
- [Install Docker](https://docs.docker.com/engine/install/)

Once you have succesfully installed Apptainer or Docker, we get started with the actual work. We apply the FreeSurfer functionalities that are included in the fMRIPrep pipeline. How to download the fMRIPrep container depends on whether you use Docker or Apptainer.

For Apptainer, run:
```
singularity build /my_images/fmriprep-<version>.simg \
                    docker://nipreps/fmriprep:<version>
```
For Docker, run:
```
docker pull nipreps/fmriprep:24.1.1
```
For more information on fMRIPrep, see the [fMRIPrep documentation](https://fmriprep.org/en/stable/)
```
--anat-only
```

## Running subsegmentations
(link to subsegmentation page)
(include extraction script in container)

## Quality Assessment part 1: Running the FS-QC pipeline
[fsqc documentation](https://deep-mi.org/fsqc/dev/index.html)

## Quality Assessment part 1: Performing a visual quality assessment
link to ENIGMA QC guide

## Data sharing
After completing all of the above steps, you're ready to share your derived data with the ENIGMA-PD core team. Please:

- Review the .csv spreadsheets for completeness, ensuring all participants are included, there are no missing or unexpected data points, and quality assessment scores have been assigned to each ROI and participant.
- Confirm whether you are authorized to share the quality check .png files. These will be used, along with your quality assessment scores, to help train automated machine learning models for ENIGMA's quality checking pipelines, to eliminate the need for manual checking in the future.

Once these checks are complete, email enigma-pd@amsterdamumc.nl to receive a personalized and secure link to a SURFdrive folder where you can temporarily upload the .csv files and, if applicable, the QA .png files. If your site has another preferred method for sharing data, please let us know, and we will try to accommodate it. We will then move the files to our central storage on the LONI server hosted by USC.
