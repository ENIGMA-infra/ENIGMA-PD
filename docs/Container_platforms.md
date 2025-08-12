## Installing containers
We will be using containerized pipelines for running FreeSurfer 7 segementation, subsegmentation and the quality control script (and potentially BIDSification). Pipeline containers are self-contained software environments that package all the tools, dependencies, and code needed to run each step of a data analysis pipeline reproducibly and consistently across systems. To download and run containers, you need a container platform, either Apptainer/Singularity or Docker. We strongly suggest Apptainer/Singularity, which is fully supported by Nipoppy. Docker can be used if you have admin rights to the computer/server you are using, or you work on something other than a Linux system (like a Mac). Using Nipoppy with Docker is possible though will likely require help -- reach out to us on our [Discord channel](https://discord.gg/dQGYADCCMB) and we would be happy to chat!

You may already have apptainer/singularity installed on your machine. You can try this by simply running `apptainer` or `singularity` in your command line and see if it throws an error. Sometimes you will need to load it to your environment, for example by running `module load apptainer`. If you don't have a container platform installed, you can find how to do this below.

### Installation
- [Install Apptainer](https://github.com/apptainer/apptainer/blob/main/INSTALL.md)
- [Install Docker](https://docs.docker.com/engine/install/)

Once you have a container platform installed, you can start building containers in the following way.
For apptainer, run:
```bash
apptainer build <pipeline>_<version>.sif \
                    docker://<repository>/<pipeline>:<version>
```
For docker, run:
```bash
docker pull <repository>/<pipeline>:<version>
```

Nipoppy encourages the use of a common directory for storing container images, which can be shared across datasets/individuals. This directory can be anywhere on a system. 

**Note:** in the global config file, `<NIPOPPY_DPATH_CONTAINERS>` should be replaced by the actual path to that directory. We encourage you to create a symlink from the `<DATASET_ROOT>/containers` directory inside the Nipoppy dataset to the shared container store location, as this would allow anyone looking at the dataset easily find the containers. In that case this substitution entry can be deleted, since by default Nipoppy will use `<DATASET_ROOT>/containers`.
