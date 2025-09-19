## Getting the Nipoppy pipeline specification files for a new pipeline

To run pipeline containers within Nipoppy, you need to download the required pipeline configuration files [from Zenodo](https://zenodo.org/communities/enigma-pd/records?q=&l=list&p=1&s=10&sort=newest). Together, these files allow Nipoppy to recognize, configure, run, and monitor the custom container image as part of its structured processing framework. You will need the following:

- `descriptor.json`
- `invocation.json`
- `config.json`
- `tracker_config.json`

A quick way to download these four files is by running: `nipoppy pipeline install --dataset <DATASET_ROOT> <ZENODO_ID>`

Please read more instructions about adding a pipeline to a dataset [on the nipoppy documentation page](https://nipoppy.readthedocs.io/en/latest/how_to_guides/pipeline_install/index.html).

**Note:** Every time a new pipeline is installed, you will need to change some paths in the global config file, depending on the pipeline.

## Examples

### fmriprep

Latest pipeline version: `fmriprep-24.1.1`

Zenodo id: 15427833

### freesurfer_subseg

Latest pipeline version: `freesurfer_subseg-1.0`

Zenodo id: 15877956

### fsqc

Latest pipeline version: `fsqc-2.1.1`

Zenodo id: 16810923
