## Getting the Nipoppy pipeline specification files for a new pipeline

You need to download the required pipeline configuration files [from the ENIGMA-PD pipelines page on Zenodo](https://zenodo.org/communities/enigma-pd/records?q=&l=list&p=1&s=10&sort=newest). Together, these files allow Nipoppy to recognize, configure, run, and monitor the custom container image as part of its structured processing framework. You will need the following:

- `descriptor.json`
- `invocation.json`
- `config.json`
- `tracker_config.json`

A quick way to download these four files is by running: `nipoppy pipeline install --dataset <DATASET_ROOT> <ZENODO_ID>`

Please read more instructions about adding a pipeline to a dataset [on the nipoppy documentation page](https://nipoppy.readthedocs.io/en/latest/how_to_guides/pipeline_install/index.html).

## Examples

### freesurfer_subseg

Latest pipeline version: `freesurfer_subseg-0.4`

Zenodo id: 15600883

### fsqc

Latest pipeline version: `fsqc-2.1.1`

Zenodo id: 16637854
