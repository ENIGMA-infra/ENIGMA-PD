# ENIGMA-PD Visual Quality Control Instructions

Welcome to the **ENIGMA-PD FreeSurfer Visual Quality Control Manual**  
*Last updated: August 2025*

This page outlines the recommended approach to visually inspect and rate FreeSurfer segmentations as part of the ENIGMA-PD project. We will assess the cortical and subcortical areas only, not the subsegmentations. 

## Step-by-step instructions for visual inspection

### 1. Download the template spreadsheets
- Download the [Cortical QC template](https://github.com/ENIGMA-PD/FS7/blob/main/docs/ENIGMA-PD_Cortical_QC_Template.xlsx)
- Download the [Subcortical QC template](https://github.com/ENIGMA-PD/FS7/blob/main/docs/ENIGMA-PD_Subcortical_QC_Template.xlsx)

These templates should be filled in manually. The only changes to be made to these templates are 1) adding all subjects from your dataset in the first column (you can copy over file names from your nipoppy manifest file), and 2) changing quality control scores from `"pass"` to `"fail"` if needed. The cortical template contains two tabs: the first tab is used to record the visual inspection scores, while the second tab provides additional context on common quality control issues observed in ENIGMA projects.  You do **not** need to review or complete the second tab — it is included to stay consistent with the standard ENIGMA consortium template. The subcortical template consists of one tab, with the selected subcortical areas for visual inspection.

### 2. Learn about the scoring

  In the template spreadsheet, all regions are by default marked as a `"pass"`. Raters are asked to provide a score for each region: **either `"pass"` or `"fail"`**, no other values should be used.
  
  **Be conservative when failing**: Use the `"fail"` label only when there are **obvious, serious issues** that would make the regional estimates **unreliable or unusable**.  Small flaws or mild asymmetries are typically not enough to justify a fail. 

#### Types of scores
There are several types of scores to complete during the **cortical** quality control: an overall score for internal and external QC, and a specific score for each region, assessed separately for the left and right hemispheres. You may optionally add comments or a QC_code (as defined in the second tab of the spreadsheet), but these are not required for the ENIGMA-PD quality assessment. The **subcortical** quality control only requires specific scores for each region, again, assessed separately for the left and right hemisphere. 

### 3. Familiarize yourself with ENIGMA quality control standards

Before starting, review the ENIGMA quality control instructions, including common segmentation errors and regions that are more prone to segmentation failure. You can find the ENIGMA manuals, adapted for the PD group below:
- [ENIGMA-PD Cortical Quality Control Manual](https://github.com/ENIGMA-PD/FS7/blob/main/docs/Cortical_QC_ENIGMA-PD_July25.pdf)
  - [Version of the cortical quiz slides including the answers to the quiz](https://github.com/ENIGMA-PD/FS7/blob/main/docs/Cortical_QC_ENIGMA-PD_July25_quiz_answers.pdf)
- [ENIGMA-PD Subcortical Quality Control Manual]()

We recommend **not focusing too heavily on the manuals**. Though they do provide some useful examples, hands-on practice is key to learning quality control, and the quality of someone’s visual assessment improves primarily through experience.

### 4. Check out the fsqc-generated html page with screenshots

Open the `fsqc-results.html` in your browser. This page shows several different images for each subject of your dataset:
- Screenshots: Internal QC of the cortical and subcortical areas
- Skullstrip:
- Surfaces:
- Hypothalamus:
- Hippocampus:


### 5. Cortical Quality Control

#### Warm-up: dynamically check a few subjects across all regions
Start by quickly scrolling through around 5–10 subjects to get a sense of the typical variability in cortical segmentations. This dynamic review helps you become familiar with how correctly segmented regions usually appear and what kinds of errors to expect.

#### For the full dataset, go per region  
Most raters prefer evaluating one cortical region at a time across all subjects. This helps with consistency and speeds up spotting systematic issues. As you go, **flag any doubtful cases**, either to revisit later or to share with the ENIGMA core team for second opinion.

### 6. Subcortical Quality Control
After the cortical regions, the subcortical quality control is a piece of cake. Subcortical regions are located close together and can usually be assessed in a single glance (in contrast to the region-by-region approach of the cortical segmentations). Segmentation errors are uncommon, and most regions should pass. Approve unless there are clear, severe distortions, which often affect multiple or all neighboring subcortical regions rather than just one.

---

### Things to Keep in Mind

- **Be lenient**: Only exclude segmentations with **clear, severe errors** that would lead to **invalid regional estimates**.  
- As you review more subjects, it becomes easier to recognize these major failures quickly.  
- **When in doubt, keep the data**, borderline cases are usually acceptable for analysis.
