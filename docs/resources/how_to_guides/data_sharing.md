# Data Sharing for ENIGMA-PD “Update to FreeSurfer 7” project

## Important things to consider
Once you have completed all the steps above, your derived data is ready to be shared with USC, where it will be accessible to the ENIGMA-PD core team and project leads (following opt-in). All data will remain on the USC server. Before transferring, please take the following steps:

- **Review the .tsv and Excel files to confirm completeness**. Verify that all participants are included, there are no missing or unexpected values, and that quality assessment scores have been assigned to each ROI and participant.
- Determine whether you are authorized to share the **quality control .png files**. These images, together with your quality assessment scores, will be used to train automated machine learning models for ENIGMA's quality checking pipelines, with the goal of reducing the need for manual review in the future.
- If your site has a preferred data transfer method (different from those described below), please let us know and we will do our best to accommodate it. Be sure to confirm this with your PI and consult your data transfer agreement beforehand.

## Data to be shared

The following data will be shared with USC as part of this project:

### MRI Outcomes (nipoppy workflow)

FreeSurfer output (5 spreadsheets)

From: `<dataset_root>/derivatives/freesurfer/7.3.2/idp/fs_stats-0.2.1/`

- Surface area: `fs7.3.2-aparc-area.tsv`

- Thickness: `fs7.3.2-aparc-thickness.tsv`

- Curvature: `fs7.3.2-aparc-meancurv.tsv`

- Subcortical volume: `fs7.3.2-aseg-volume.tsv`


From: `<dataset_root>/derivatives/freesurfer_subseg/1.0/idp/fs_subseg_stats-0.2/`

- Subsegmentations: `subsegmentation_volumes.tsv`

Quality control output (2 spreadsheet, optionally .png files)

- Cortical quality assessment scores

- Subcortical quality assessment scores

- Quality control .png files (if authorized)

### Clinical and Demographic Data
- 1 spreadsheet containing clinical and demographic variables for all participants

- 1 data dictionary created [using Neurobagel](/neurobagel.md)

## Data sharing protocols

### Option A: Sites without a Data Transfer Agreement (DTA) or similar agreement

Important: This upload method uses a shared account. In principle, any site with the login credentials can browse, download, or interact with data uploaded by other sites. Only use this route if you are comfortable with your data being visible to other ENIGMA-PD working group members. If your site has a DTA in place, this route is likely not permitted under that agreement, please use Option B instead.

Login details are not public and are only shared with ENIGMA-PD sites that have reached out to us directly. The username is enigma_pd. To receive the password, please email us at ENIGMA-PD@amsterdamumc.nl.

#### Option A1: Upload via graphical interface, for example Filezilla (drag-and-drop)
Open your preferred tool and connect using the following details:

- Host: (request via ENIGMA-PD@amsterdamumc.nl)

- Username: (request via ENIGMA-PD@amsterdamumc.nl)

- Password: (request via ENIGMA-PD@amsterdamumc.nl)

- Port: (request via ENIGMA-PD@amsterdamumc.nl)

Once connected, you should be in `/ftphome/enigma_pd/`. Find the folder prepared for your site (e.g. AMS2) and drag and drop your files into it.

#### Option A2: Upload via command line
Open a terminal and log on to the USC server (request log-in details via ENIGMA-PD@amsterdamumc.nl)

This places you in `/ftphome/enigma_pd/`. Navigate to the folder prepared for your site, for example:
`cd AMS2`

Upload a single file: `put AMS2.tsv`
Upload a folder: `put -r AMS2`

**Note:**
When logging in, you might get an error that looks like this:
```
Unable to negotiate with 10.2.2.175 port 22: no matching host key type found.
Their offer: ssh-rsa,ssh-dss
```
If that is the case, on your local machine, navigate to:
`cd /etc/ssh/`

Then use a text editor like vim to amend the ssh_config file (you may need to use sudo and add in your machine password):
`sudo vim ssh_config`

Add these two lines at the bottom of the config when in insert mode (press "i")                                                                  
```
HostkeyAlgorithms +ssh-rsa  
PubkeyAcceptedAlgorithms +ssh-rsa 
```
Save the config file using by pressing esc, then typing :wq! (include the colon). Try again once that is saved.

### Option B: Sites with a Data Transfer Agreement (DTA)
If your site has a DTA in place, the shared SFTP route above is likely not an approved method of transfer, as it does not prevent other sites from accessing your data. Therefore, we also provide the possibility to send the data securely and encrypted using [SURFfilesender](https://www.surf.nl/en/services/storage-data-management/surffilesender). 

#### Option B1: Upload files via browser
For this, you can use the personal invitation link that you received by email. This email has been sent from **SURFfilesender \<noreply@surf.nl\>** on behalf of our team, so please check your spam or junk folder if you do not see it in your inbox. The email will contain a voucher link and will look something like this:
>*"Please find below a voucher which grants access to SURFfilesender. You can use this voucher to upload one set of files and make it available for download."*

The voucher link will be valid for 60 days, so please use it in time. If you did not receive the email, cannot find it, or need a new link, please reach out to us at ENIGMA-PD@amsterdamumc.nl.

#### Option B2: Upload via command line

This option is available if you have a SURF account (available to all Dutch educational institutions) or an eduID (a guest account for SURF services). If you do not have either, you can request an eduID at [eduid.nl](eduid.nl). Full instructions for setting up and using the SURF CLI client can be found [here](https://servicedesk.surf.nl/wiki/spaces/WIKI/pages/198967770/SURFfilesender+CLI+client). In short, the process involves downloading the Python CLI client from your SURFfilesender profile page, installing a few standard Python dependencies (which are present on most systems), configuring the client with your username and API key from the same profile page, and then running the client with the recipient address and file path to upload your data.
