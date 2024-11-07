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

Resources from the BIDS community offer guidance on organizing your data, and BIDS converters can help automate this process, saving time and reducing manual errors. We recommend using Dcm2Bids (for DICOM's) and BIDScoin (for NIfTI's). Resources:
- [BIDS documentation](https://bids-website.readthedocs.io/en/latest/index.html)
- [Recommended converter; BIDScoin](https://bidscoin.readthedocs.io/en/stable/)
- [BIDS tutorials](https://www.youtube.com/watch?v=pAv9WuyyF3g&list=PLtJYlrqQ3YK_M4YgkUx6akJqlHF1R7A5g)

## Nipoppyfication
insert background; why important?
[Nipoppy documentation](https://nipoppy.readthedocs.io/en/latest/index.html)

## Running FreeSurfer 7
The first step of running FS7 is to prepare your work environment with either Apptainer or Docker. We prefer Apptainer, but Docker can be used if you don't have access to a Linux system.

[Install Apptainer](https://github.com/apptainer/apptainer/blob/main/INSTALL.md)

[Install Docker](https://docs.docker.com/engine/install/)

Once you have succesfully installed Apptainer or Docker, we can finally start with the actual work. We apply the FreeSurfer tools that are included in the fMRIPrep pipeline. How to download the fMRIPrep container depends on whether you use Docker or Apptainer.

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

## Quality Check; running fsqc
[fsqc documentation](https://deep-mi.org/fsqc/dev/index.html)
linkt to ENIGMA QC guide

## Data sharing
SURFdrive?
