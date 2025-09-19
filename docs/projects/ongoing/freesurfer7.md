# Welcome to the ENIGMA-PD FreeSurfer 7 guidelines!

This page is created to guide collaborating ENIGMA-PD sites through the FreeSurfer processing steps. The outcomes include cortical thickness, cortical surface area, and volume of subcortical regions and their subfields. All steps and code required are combined into the guidelines presented here. If you have any questions, concerns, or issues, please contact the ENIGMA-PD core team at enigma-pd@amsterdamumc.nl. 

## Leaderboard
To help motivate and monitor each site's progress, we maintain a leaderboard that outlines all the steps detailed in these guidelines. If you are in charge of data processing at your site, please request access and regularly update your progress on the current steps on the [ENIGMA-PD Leaderboard](https://docs.google.com/spreadsheets/d/13iGfh-97ZYnAyjT5egBDHmGhqXbsl1yo1A6QnPXQYbY/edit?usp=sharing).

## Overview
The figure shows the expected outcomes and corresponding processing steps - most of which can be performed using the Nipoppy framework and helper Python package. We strongly recommend adoption of Nipoppy tools to simplify coordination and ensure reproducibility of this end-to-end process across all sites. 
![enigma-nipoppy-FS7-upgrade-overview](https://github.com/user-attachments/assets/aae8449c-58cf-4889-92de-979f79082e28)

## Setting up Nipoppy
Nipoppy is a lightweight framework for standardized data organization and processing of neuroimaging-clinical datasets. Its goal is to help users adopt the [FAIR principles](https://www.go-fair.org/fair-principles/) and improve the reproducibility of studies. 

The ongoing collaboration between the ENIGMA-PD team and Nipoppy team has streamlined data curation, processing, and analysis workflows, which significantly simplifies tracking of data availability, addition of new pipelines and upgrading of existing pipelines. The ENIGMA-PD and Nipoppy team is available to support and guide users through the process of implementing the framework, ensuring a smooth transition. To join the Nipoppy support community, we recommend joining their [Discord channel](https://discord.gg/dQGYADCCMB). Here you can ask questions and find answers while working with Nipoppy. 

**Here, primairly we will use Nipoppy to help you with 1) BIDSification, 2) FreeSurfer7 processing, 3) Sub-segmentation and 4) Quality control.** 

For more information, see the [Nipoppy documentation](https://nipoppy.readthedocs.io/en/stable/index.html).

### Getting started
To install Nipoppy, we refer to the [Installation page](https://nipoppy.readthedocs.io/en/stable/overview/installation.html). 

Once Nipoppy is successfully installed, you will need to create a Nipoppy dataset and populate it with your data. There are a few different starting points depending on the current state of your dataset. If you have your data already in BIDS format, click [here](#starting-with-bidsified-data). If you have DICOM of NIFTI files that are not yet in BIDS, continue below. If you're not sure what BIDS is or if you're wondering why you should convert your data into BIDS at all, you can find more info [here](../resources/BIDS_info.md).

#### Starting from source data (either DICOMs or NIfTIs that are *not yet* in BIDS)

This is the scenario assumed by the Nipoppy [Quickstart page](https://nipoppy.readthedocs.io/en/stable/overview/quickstart.html). Follow this guide to:
1. Create an empty Nipoppy dataset (i.e. directory tree)
2. Write a manifest file representing your data
3. Modify the global config file with paths to e.g., path to your container directory

Note: if your dataset is cross-sectional (i.e. only has one session), you still need to create a `session_id` for the manifest. In this case the value would be the same for all participants.

When you reach the end of the Quickstart, it is time to [copy and reorganize](https://nipoppy.readthedocs.io/en/stable/how_to_guides/user_guide/organizing_imaging.html) your raw imaging data to prepare them for BIDS conversion. Once this is done, you can find how to perform the BIDSification within the Nipoppy framework [here](https://nipoppy.readthedocs.io/en/stable/how_to_guides/user_guide/bids_conversion.html). We recommend applying a containerized BIDS-conversion pipeline that can be run within Nipoppy. [Here](../resources/Container_platforms.md) you can find how to download containers and [here](../resources/getting_ENIGMA-PD_pipeline_config_files.md) you can find how to run them within Nipoppy.

#### Starting with BIDSified data

If your dataset is already in BIDS, then the manifest-generation step can be skipped by initializing the Nipoppy dataset with this command, specifying the path to your new dataset and the path to your existing BIDS data:

```bash
nipoppy init --dataset <dataset_root> --bids-source <path_to_existing_bids_data>
```

This command will create a Nipoppy dataset (i.e. directory tree) from preexisting BIDS dataset and automatically generate a manifest file for you! 

##### BIDS datasets without sessions
If the existing BIDS data does not have session-level folders, Nipoppy will create "dummy sessions" (called `unnamed`) in the manifest. This is because the Nipoppy manifest still requires a non-empty `session_id` value when imaging data is available for a participant.

If it is feasible to redo the BIDSification to include session folders, we recommend doing so since this is considered good practice. Otherwise, Nipoppy can still be run, but you will need to make some manual changes. For more information, see [here](https://nipoppy.readthedocs.io/en/stable/how_to_guides/init/bids.html#bids-data-without-sessions)

#### Starting from data already processed with FreeSurfer7

We still encourage you to use Nipoppy to organize your source and/or BIDS data with your processed FS7 output to make use of automated trackers and downstream subsegmentation processing. However, you may need to some help depending on your version of FreeSurfer and naming convention of `participant_id`. Reach out to us on our [Discord channel](https://discord.gg/dQGYADCCMB) and we would be happy to help! 

## Running FreeSurfer 7
When you reach this point, the hardest part is behind you and we can finally come to the real stuff. We will run FreeSurfer 7 through fMRIPrep using Nipoppy. See [here](https://nipoppy.readthedocs.io/en/latest/how_to_guides/user_guide/processing.html) for additional information about running processing pipelines with Nipoppy.

We will apply the FreeSurfer functionalities that are included in the fMRIPrep pipeline. We assume here that you have Apptainer installed as your container platform (see [here](../resources/Container_platforms.md) for more info and how to get it). Now, you can pull the fMRIPrep container in the following way:

```bash
apptainer build fmriprep_24.1.1.sif \
                    docker://nipreps/fmriprep:24.1.1
```

Make sure that you have the fMRIPrep container stored in the containers folder that you reference to in your global config file.

For more information on fMRIPrep, see the [fMRIPrep documentation](https://fmriprep.org/en/stable/)

### Setting up configuration
Next, we will need to install the fMRIPrep pipeline within Nipoppy. You can do this by simply running:

```bash
nipoppy pipeline install --dataset <dataset_root> 15427833
```

15427833 is the Zenodo ID for the Nipoppy configuration files for fmriprep 24.1.1. Read more about this step [here](../resources/getting_ENIGMA-PD_pipeline_config_files.md).

Once the pipeline is installed, open the global config file and check whether the correct fMRIPrep version is included under `PIPELINE_VARIABLES`.
The following paths should be replaced here under the correct version of the fMRIPrep pipeline in the global config file:
- `<FREESURFER_LICENSE_FILE>` (required to run FreeSurfer; you can get a FreeSurfer licence for free at [the FreeSurfer website](https://surfer.nmr.mgh.harvard.edu/registration.html))
- `<TEMPLATEFLOW_HOME>` (see [here](../resources/Templateflow_info.md) for more info on Templateflow)

### Run pipeline
Finally, simply run the following line of code:
```bash
nipoppy process --pipeline fmriprep --pipeline-version 24.1.1 --dataset <dataset_root>
```
This should initiate the FS7 segmentation of your T1-weighted images! 

**Note:** the command above will run all the participants and sessions in a loop, which may be inefficient. If you're using an HPC, you may want to submit a batch job to process all participants/sessions. Nipoppy can help you do this by
1. Generate a list of "remaining" participants to be processed for your job-subission script: `nipoppy process --pipeline fmriprep --pipeline-version 24.1.1 --dataset <dataset_root> --write-list <path_to_participant_list>`
2. Automatically submit HPC jobs for you with additional configuration (more info [here](https://nipoppy.readthedocs.io/en/latest/how_to_guides/parallelization/hpc_scheduler.html))

### Track pipeline output

The `nipoppy track-processing` command can help keep track of which participants/sessions have all the expected output files for a given processing pipeline. See [here](https://nipoppy.readthedocs.io/en/latest/how_to_guides/user_guide/tracking.html) for more information. Running this command will update the `processing_status.tsv` under the `derivatives` folder.

### Extract pipeline output

For automatic extraction of the cortical thickness, cortical surface area and subcortical volume into .tsv files, you can use another [Nipoppy pipeline](../resources/getting_ENIGMA-PD_pipeline_config_files.md), called fs_stats. The Zenodo ID for this pipeline is 15427856, so you can install it with the following command:
```bash
nipoppy pipeline install --dataset <dataset_root> 15427856
```
Remember to define the freesurfer licens file path in your global config file under the newly installed pipeline. Then, you can simply run 
```bash
nipoppy extract --pipeline fs_stats --dataset <dataset_root>
```
to get things going. You can find the extracted data under `<dataset_root>/derivatives/freesurfer/7.3.2/idp/`.

Once FS7 processing and extraction has completed, you can move on to the subsegmentations.

---

## Running the FreeSurfer subsegmentations
🎉 **It’s go time!**  
The **subsegmentations pipeline** is now ready to be run! Since you’ve all just been through fMRIPrep in Nipoppy, this next step will feel familiar as running this pipeline follows a very similar workflow.

**About the pipeline:**
This pipeline uses existing FreeSurfer 7 functionalities to extract subnuclei volumes from subcortical regions like the *thalamus*, *hippocampus*, *brainstem*, *hypothalamus*, *amygdala*, and *hippocampus*. It requires completed FreeSurfer output (`recon-all`) and integrates the subsegmentation outputs directly into the existing `/mri` and `/stats` directories. Additionally, the pipeline will perform [Sequence Adaptive Multimodal SEGmentation (SAMSEG)](https://surfer.nmr.mgh.harvard.edu/fswiki/Samseg) on T1w images in order to calculate a superior intracranial volume.

### Pulling the Docker image

You need to download the container image that will run the subsegmentations. Use the following Apptainer command to pull the image from Docker Hub:

```bash
apptainer build freesurfer_subseg_1.0.sif docker://nichyconsortium/freesurfer_subseg:1.0
```

Make sure the resulting image file is placed in the container directory referenced in your global config file.

### Getting the Nipoppy pipeline specification files for this pipeline
To get the Nipoppy specification files for the subsegmentation container, run:
```bash
nipoppy pipeline install --dataset <dataset_root> 15877956
```

Read more about this step [here](../resources/getting_ENIGMA-PD_pipeline_config_files.md).

**Note:** If you have multiple T1w images per subject per session, the container will throw an error. In this case, you will need to open the invocation file under `<dataset_root>/pipelines/processing/freesurfer_subseg-1.0/` and specify the name of the desired T1w image for SAMSEG in the following way:
```
"t1_image_path": "[[NIPOPPY_BIDS_PARTICIPANT_ID]]_[[NIPOPPY_BIDS_SESSION_ID]]_<edit-me>_T1w.nii.gz"
```

### Change your global config file
Open the global config file and add the path to your freesurfer license file under the freesurfer_subseg pipeline, just like you did for the fMRIPrep pipeline:

```json
"PIPELINE_VARIABLES": {
  "BIDSIFICATION": {},
  "PROCESSING": {
    "fmriprep": {
      "24.1.1": {
        "FREESURFER_LICENSE_FILE": "path/to/license/file/license.txt",
        "TEMPLATEFLOW_HOME": "path/to/templateflow/"
      }
    },
    "freesurfer_subseg": {
      "1.0": {
        "FREESURFER_LICENSE_FILE": "path/to/license/file/license.txt"
      }
    }
  }
}
```

#### Final check

Before trying to run the pipeline, confirm that the pipeline is recognized by running `nipoppy pipeline list`. This will print a list of the available pipelines.

### Running the pipeline

To run the subsegmentation pipeline, use the following command:

```bash
nipoppy process --pipeline freesurfer_subseg --pipeline-version 1.0 --dataset <dataset_root>
```

### Tracking pipeline output

Use the `nipoppy track-processing` command to check which participants/sessions have complete output:

```bash
nipoppy track-processing --pipeline freesurfer_subseg --dataset <dataset_root>
```

This helps you confirm whether the pipeline ran successfully across your dataset (again, check `processing_status.tsv` under the `derivatives` folder).

### Extracting pipeline output

The pipeline for extraction of data from the subsegmentation is under construction. Stay tuned for updates! You can already extract data from the standard FreeSurfer 7 segementation (see [here](#extract-pipeline-output)) and continue with running the fsqc toolbox as described below.

---

## Quality Assessment part 1: Running the FS-QC toolbox
Congratulations, you made it to the quality assessment! For this purpose, we will use FreeSurfer Quality Control (FS-QC) toolbox. The [FS-QC toolbox](https://github.com/Deep-MI/fsqc) takes existing FreeSurfer (or FastSurfer) output and computes a set of quality control metrics. These will be reported in a summary table and/or .html page with screenshots to allow for visual inspection of the segmentations.

### Pulling the Docker image

You need to download the container image that will run the freesurfer quality control pipeline. Use the following command to pull the image from Docker Hub:

```bash
apptainer build fsqc_2.1.4.sif docker://deepmi/fsqcdocker:2.1.4
```

Make sure the resulting image file is placed in the container directory referenced in your global Nipoppy configuration.

### Getting the Nipoppy pipeline specification files for this pipeline
To get the Nipoppy specification files for the FS-QC container, run:
```bash
nipoppy pipeline install --dataset <dataset_root> 17100133
```

Read more about this step [here](../resources/getting_ENIGMA-PD_pipeline_config_files.md).

### Change your global config file
Open the global config file and add the correct freesurfer version (7.3.2) under the fsqc pipeline.

#### Final check

Before trying to run the pipeline, confirm that the pipeline is recognized by running `nipoppy pipeline list`. This will print a list of the available pipelines.

### Running the pipeline

To run the subsegmentation pipeline, use the following command:

```bash
nipoppy process --pipeline fsqc --pipeline-version 2.1.4 --pipeline-step process --dataset <dataset_root>
```

### Expected FS-QC output

After running the command, you will find all results inside the derivatives folder. The output will include:

- **Several folders**, most of them corresponding to the flags used in the command, such as: `screenshots`, `surfaces`, `skullstrip`, `hypothalamus`, `hippocampus`, and also, `status`, `metrics`

- **A CSV file** (`fsqc-results.csv`) summarizing quantitative quality control metrics for all subjects.

- **A main HTML summary file** (`fsqc-results.html`) that aggregates all subject screenshots for easy visual inspection.

You can verify that images were created for all subjects by running

```bash
nipoppy track-processing --pipeline fsqc --pipeline-step process-tracking --dataset <dataset_root>
```
and checking `processing_status.tsv` under the `derivatives` folder.

#### Important notes for viewing and copying files:

##### Locally
- We **strongly recommend downloading the entire output folder locally** before opening the HTML file. Opening the HTML on a server or network drive is often slow and may cause images not to load properly.

- When copying files, **make sure to include all generated folders** (such as `screenshots`, `surfaces`, etc.) along with the `fsqc-results.html` file. These folders contain the images referenced in the HTML and are essential for proper display.

##### On the server
- If you have not experienced such issues before and prefer to work directly on your server, you can instead open the HTML file in your available browser (for example: `firefox fsqc-results.html`).

##### Final check
- When opening the `fsqc-results.html` file:  
  - Scroll through the subjects to confirm all images load and no data is missing.  
- Click on any image to zoom in, or right-click and choose “Open in new tab” and inspect details more closely.

---

## Quality Assessment part 2: Performing a visual quality assessment
Quality checking is essential to make sure the output that you have produced is accurate and reliable. Even small errors or artifacts in images can lead to big mistakes in analysis and interpretation, so careful checks help us to verify whether we can savely include a certain region of interest or participant in our analysis. For the FreeSurfer output, we will follow standardized ENIGMA instructions on how to decide on the quality of the cortical and subcortical segmentations. **At this stage, visual quality assessment of the subsegmentations (e.g., thalamic or hippocampal nuclei) is not required, as there are no established protocols yet and the process would be highly time-consuming; statistical checks (e.g., outlier detection) can be used instead. This may be followed up at a later stage, once there is a project that specifically focuses on these outcomes and the necessary anatomical expertise is available to develop a dedicated quality control manual.**

You can find the updated ENIGMA-PD QC instructions for visual inspection [here](../resources/ENIGMA-PD_visual_QC_instructions.md).

---

## Data sharing
After completing all of the above steps, you're ready to share your derived data with the ENIGMA-PD core team. Please:

- Review the .tsv and Excel spreadsheets for completeness, ensuring all participants are included, there are no missing or unexpected data points, and quality assessment scores have been assigned to each ROI and participant.
- Confirm whether you are authorized to share the quality check .png files. These will be used, along with your quality assessment scores, to help train automated machine learning models for ENIGMA's quality checking pipelines, to eliminate the need for manual checking in the future.

Once these checks are complete, email enigma-pd@amsterdamumc.nl to receive a personalized and secure link to a SURFdrive folder where you can temporarily upload the .csv files and, if applicable, the QA .png files. If your site has another preferred method for sharing data, please let us know, and we will try to accommodate it. We will then move the files to our central storage on the LONI server hosted by USC.