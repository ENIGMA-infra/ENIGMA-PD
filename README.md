# Welcome to the ENIGMA-PD FreeSurfer 7 guidelines!

This page is created to guide collaborating ENIGMA-PD sites through the FreeSurfer processing steps. The outcomes include cortical thickness, cortical surface area, and volume of subcortical regions and their subfields. All steps and code required are combined into the guidelines presented here. If you have any questions, concerns, or issues, please contact the ENIGMA-PD core team at enigma-pd@amsterdamumc.nl. 

## Leaderboard
To help motivate and monitor each site's progress, we maintain a leaderboard that outlines all the steps detailed in these guidelines. If you are in charge of data processing at your site, please request access and regularly update your progress on the current steps on the [ENIGMA-PD Leaderboard](https://docs.google.com/spreadsheets/d/13iGfh-97ZYnAyjT5egBDHmGhqXbsl1yo1A6QnPXQYbY/edit?usp=sharing).

## Nipoppyfication
Nipoppy is a lightweight framework for standardized organization and processing of neuroimaging-clinical datasets. Its goal is to help users adopt the FAIR principles and improve the reproducibility of studies. Essentially an extension of BIDS, Nipoppy builds on the BIDS standard to enhance data organization, processing, and integration, further supporting standardized workflows and reproducible research practices.

![Nipoppy framework](https://raw.githubusercontent.com/nipoppy/nipoppy/main/docs/source/_static/img/nipoppy_protocol.jpg)

The ongoing collaboration between the ENIGMA-PD team and Nipoppy developers has significantly improved dataset organization for the Amsterdam and open datasets. It has also streamlined the standardization of analysis workflows, made re-running pipelines for version updates easier, and simplified tracking of which datasets have been processed with specific analysis pipelines. The ENIGMA-PD and Nipoppy team is available to support and guide users through the process of implementing the framework, ensuring a smooth transition. For more information, see the [Nipoppy documentation](https://nipoppy.readthedocs.io/en/latest/index.html).

To install Nipoppy, we refer to the [Installation page](https://nipoppy.readthedocs.io/en/latest/installation.html). Once Nipoppy is succesfully installed, please follow all steps listed on the [Quickstart page](https://nipoppy.readthedocs.io/en/latest/quickstart.html). In the global config file, you will need to add the path to a FreeSurfer license. You can get a FreeSurfer licence for free at [the FreeSurfer website](https://surfer.nmr.mgh.harvard.edu/registration.html). When you reach the end of the Quickstart, it is time to copy and [reorganize](https://nipoppy.readthedocs.io/en/latest/user_guide/organizing_imaging.html) your raw imaging data. The next step is converting your data to the BIDS standard.

## BIDSification
Before starting the analysis, organizing your data is essential — it will benefit this analysis and streamline any follow-up ENIGMA-PD work. We know it can be challenging, but we’re here to support you. The Brain Imaging Data Structure (BIDS) format is a standardized format for organizing and labeling neuroimaging data to ensure consistency and make data easily shareable and analyzable across studies. Although we’re focusing on T1-weighted images for this analysis, organizing available diffusion-weighted or functional MRI data in BIDS will make future analyses easier.

Here are the core principles for organizing your neuroimaging data in BIDS format:
- Use consistent file and folder names
- Separate modalities
- Include metadata files
- Validate the structure

Resources from the BIDS community offer guidance on organizing your data, and BIDS converters can help automate this process, saving time and reducing manual errors. We recommend using Dcm2Bids (for DICOM's) and BIDScoin (for NIfTI's).
- [BIDS documentation](https://bids-website.readthedocs.io/en/latest/index.html)
- [Recommended converter; BIDScoin](https://bidscoin.readthedocs.io/en/stable/)
- [BIDS tutorials](https://www.youtube.com/watch?v=pAv9WuyyF3g&list=PLtJYlrqQ3YK_M4YgkUx6akJqlHF1R7A5g)

[Here](https://nipoppy.readthedocs.io/en/latest/user_guide/bids_conversion.html) you can find how to perform the BIDSification within the Nipoppy framework (recommended).

## Running FreeSurfer 7
When you reach this point, the hardest part is behind you and we can finally come to the real stuff. The first step of running FS7 is to prepare your work environment with either Apptainer or Docker. We prefer Apptainer, but Docker can be used if you don't have admin rights or access to a Linux system.

### Installation
- [Install Apptainer](https://github.com/apptainer/apptainer/blob/main/INSTALL.md)
- [Install Docker](https://docs.docker.com/engine/install/)

We will apply the FreeSurfer functionalities that are included in the fMRIPrep pipeline. Once you have succesfully installed Apptainer or Docker, you can pull the fMRIPrep container. How to do this depends on whether you use Docker or Apptainer.

For Apptainer, run:
```
singularity build /my_images/fmriprep-<version>.simg \
                    docker://nipreps/fmriprep:24.1.1
```
For Docker, run:
```
docker pull nipreps/fmriprep:24.1.1
```
For more information on fMRIPrep, see the [fMRIPrep documentation](https://fmriprep.org/en/stable/)

### Setting up configuration
Make sure that you have the fMRIPrep container stored in the containers folder that you reference to in your global config file. 
Next, open the global config file, check whether the correct fMRIPrep version is included under PROC_PIPELINES, and add `--anat-only` under ARGS (we are not interested in processing functional scans for now).

### Run pipeline
Finally, simply run the following line of code, specifying the path to your dataset root.
```
nipoppy run --pipeline fmriprep --pipeline-version 24.1.1 [dataset_root]
```
This should initiate the FS7 segmentation of all your T1-weighted images! Once processing has completed, you can move on to the subsegmentations.

## Running subsegmentations
<@Eva to complete>
(link to subsegmentation page)
(include extraction script in container)

## Quality Assessment part 1: Running the FS-QC toolbox
The [FreeSurfer Quality Control (FS-QC) toolbox](https://github.com/Deep-MI/fsqc) takes existing FreeSurfer or FastSurfer output and computes a set of quality control metrics. These will be reported in a summary table and/or .html page with screenshots to allow for visual inspection of the segmentations.

### Getting the container
For Apptainer:
- Go to a path where you want the image (.sif) to be saved and create the image using the docker tag. Check the [latest tags](https://hub.docker.com/r/deepmi/fsqcdocker/tags) on the fsqc docker hub. Creating the image takes <3 min.
```
cd /path/to/your/containers
```
```
apptainer build fsqc-latest.sif docker://deepmi/fsqcdocker:latest
```
- Print the command usage to test if you can run the container
```
apptainer run /path/to/fsqc-latest.sif
```

### Running the FS-QC command
Please read more about the required and optional arguments [here](FS-QC.md). For ENIGMA-PD, we ask you to run the command below to produce several screenshots at different slices and also include the subsegmentations. 

For Apptainer, adjust the paths to the FreeSurfer output directory and container directory and run:
```
apptainer run --bind /path/to/FreeSurfer/output/dir/:/data_fsqc \
/path/to/container/fsqc-latest.sif \
--subjects_dir /data_fsqc/ \
--output_dir /data_fsqc/fsqc_output_aparc_aseg \
--screenshots-html \
--screenshots_overlay aparc+aseg.mgz \
--screenshots_views x=-20 x=-10 x=10 x=20 y=-10 y=0 y=10 y=20 z=0 z=10 z=20 z=30 \
--screenshots_layout 3 4 \
--surfaces-html \
--skullstrip-html \
--hypothalamus-html \
--hippocampus-html \
--hippocampus-label T1.v22 \
--outlier
```

## Quality Assessment part 2: Performing a visual quality assessment
@Eva to complete
[link to ENIGMA QC guide](https://drive.google.com/file/d/1P4z42tNPRwwX3U7-L_wsPkxsatGLZaCJ/edit?pli=1)

## Data sharing
After completing all of the above steps, you're ready to share your derived data with the ENIGMA-PD core team. Please:

- Review the .csv spreadsheets for completeness, ensuring all participants are included, there are no missing or unexpected data points, and quality assessment scores have been assigned to each ROI and participant.
- Confirm whether you are authorized to share the quality check .png files. These will be used, along with your quality assessment scores, to help train automated machine learning models for ENIGMA's quality checking pipelines, to eliminate the need for manual checking in the future.

Once these checks are complete, email enigma-pd@amsterdamumc.nl to receive a personalized and secure link to a SURFdrive folder where you can temporarily upload the .csv files and, if applicable, the QA .png files. If your site has another preferred method for sharing data, please let us know, and we will try to accommodate it. We will then move the files to our central storage on the LONI server hosted by USC.
