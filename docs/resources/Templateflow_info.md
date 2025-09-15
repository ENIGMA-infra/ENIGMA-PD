#### Clarifications about Templateflow

[Templateflow](https://www.templateflow.org/) is a library of neuroimaging templates (e.g. `MNI152NLin2009cAsym`) used by several popular processing pipelines, including fMRIPrep (which we are using to run FreeSurfer 7) and MRIQC.

By default the templates are stored in `~/.templateflow`, but in general it is a good idea to store them somewhere more central/visible, so that the same templates can be used by different people in a research group. Another reason to specify another path is that the home directory often has limited storage on some servers.
  - In the Nipoppy global config file, `<PATH_TO_TEMPLATEFLOW_DIRECTORY>` should be replaced by the *path to an empty directory*, possibly in a similar location as (parallel to) the container store directory.

The first time fMRIPrep is run, it will attempt to download templates to the Templateflow directory, which will require the computer to be connected to the internet. If you are running fMRIPRep on a cluster where compute nodes do not have access to the Internet, see [here](https://fmriprep.org/en/24.1.1/faq.html#how-do-you-use-templateflow-in-the-absence-of-access-to-the-internet) and feel free to reach out to us for help.
