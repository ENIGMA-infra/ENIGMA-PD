# About the FreeSurfer Quality Control Toolbox (FS-QC)

The [FreeSurfer Quality Control (FS-QC) toolbox](https://github.com/Deep-MI/fsqc) takes existing FreeSurfer or FastSurfer output and computes a set of quality control metrics. These will be reported in a summary table and/or .html page with screenshots to allow for visual inspection of the segmentations.

## Command usage
Type `apptainer run /path/to/fsqc-latest.sif` to print the command usage and options.

**Required arguments:**
```
 --subjects_dir <directory>               subjects directory with a set of Freesurfer processed individual datasets.
  --output_dir <directory>                output directory
```

**Optional arguments:**
```
 --subjects SubjectID [SubjectID ...]     list of subject IDs. If omitted, all suitable sub-directories within the subjects directory will be used.
  --subjects-file <filename>              filename with list of subject IDs (one per line). If omitted, all suitable sub-directories within the subjects directory will be used.
  --shape                                 run shape analysis
  --screenshots                           create screenshots of individual brains
  --screenshots-html                      create screenshots of individual brains with html summary page
  --surfaces                              create surface plots of individual brains
  --surfaces-html                         create surface plots of individual brains with html summary page
  --surfaces_views SURFACES_VIEWS [SURFACES_VIEWS ...]
                                          specify camera views for surface images. Choose from: anterior, posterior, left, right, superior, inferior
  --skullstrip                            create brainmask plots of individual brains
  --skullstrip-html                       create brainmask plots of individual brains with html summary page
  --fornix                                check fornix segmentation
  --fornix-html                           check fornix segmentation and create html summary page
  --hypothalamus                          check hypothalamus segmentation
  --hypothalamus-html                     check hypothalamus segmentation and create html summary page for evaluation
  --hippocampus                           check hippocampus segmentation
  --hippocampus-html                      check hippocampus segmentation and create html summary page for evaluation
  --hippocampus-label <string>
                                          specify custom label for hippocampal segmentation files
  --outlier                               run outlier detection
  --outlier-table <filename>
                                          specify normative values
  --fastsurfer                            use FastSurfer output
  --exit-on-error                         terminate the program when encountering an error
```

**Expert arguments:**
```
  --screenshots_base <base image for screenshots>                                        base image for screenshots
  --screenshots_overlay <overlay image for screenshots>                                  overlay image for screenshots
  --screenshots_surf <surface(s) for screenshots> [<surface(s) for screenshots> ...]     surface(s) for screenshots
  --screenshots_views <dimension=coordinate> [<dimension=coordinate> ...]                view specification for screenshots
  --screenshots_layout <num> <num>                                                       layout for screenshots
```
