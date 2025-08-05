## ENIGMA-PD Visual Quality Control Instructions

Welcome to the **ENIGMA-PD FreeSurfer Visual Quality Control Manual**  
*Last updated: July 2025*

This guide outlines the recommended approach to visually inspect and rate FreeSurfer segmentations as part of the ENIGMA-PD project. We will assess the cortical and subcortical areas only, not the subsegmentations. 

### Download the template spreadsheets
- Download the [Cortical_template](https://github.com/ENIGMA-PD/FS7/blob/main/docs/ENIGMA-PD_Cortical_QC_Template.xlsx)
- Download the [Subcortical template]()

These templates should be filled in manually. The cortical template contains two tabs: the first tab is used to record the visual inspection scores, while the second tab provides additional context on common quality control issues observed in ENIGMA projects.  You do **not** need to review or complete the second tab — it is included to stay consistent with the standard ENIGMA consortium template.

### Step-by-step instructions for visual inspection

1. **Learn about the scoring**

  In the template spreadsheet, all regions are by default marked as a `"pass"`. Raters are asked to provide a score for each region: **either `"pass"` or `"fail"`**, no other values should be used.
  
  **Be conservative when failing**: Use the `"fail"` label only when there are **obvious, serious issues** that would make the regional estimates **unreliable or unusable**.  Small flaws or mild asymmetries are typically not enough to justify a fail.
  
  There are two types of scores to complete during quality control: an overall score for external QC, and a specific score for each region, assessed separately for the left and right hemispheres. By the end of the QC process, every region must have a score with **no empty cells left** in the spreadsheet.
  You may optionally add comments or a QC_code (as defined in the second tab of the spreadsheet), but these are not required for the ENIGMA-PD quality assessment.

2. **Familiarize yourself with ENIGMA quality control standards**  

Before starting, review the ENIGMA quality control instructions below, including common segmentation errors and regions that are more prone to segmentation failure. You can find the ENIGMA manual, adapted for the PD group [here](https://github.com/ENIGMA-PD/FS7/blob/main/docs/Cortical_QC_ENIGMA-PD_July25.pdf) and a version including the powerpoint notes (i.e. answers to the quiz) [here](https://github.com/ENIGMA-PD/FS7/blob/main/docs/Cortical_QC_ENIGMA-PD_July25_quiz_answers.pdf). We recommend not focusing too heavily on the manual. Though it does provide some useful examples, hands-on practice is key to learning quality control, and the quality of someone’s visual assessment improves primarily through experience.

3. **Warm-up: dynamically check a few subjects across all regions**  

Start by quickly scrolling through around 5–10 subjects to get a sense of the typical variability in segmentations. This dynamic review helps you become familiar with how correctly segmented regions usually appear and what kinds of errors to expect.

4. **For the full dataset, go per region**  

Most raters prefer evaluating one region at a time across all subjects. This helps with consistency and speeds up spotting systematic issues. As you go, **flag any doubtful cases**, either to revisit later or to share with the ENIGMA core team for second opinion.

---

### Things to Keep in Mind

- **Be lenient**: Only exclude segmentations with **clear, severe errors** that would lead to **invalid regional estimates**.  
- As you review more subjects, it becomes easier to recognize these major failures quickly.  
- **When in doubt, keep the data**, borderline cases are usually acceptable for analysis.
