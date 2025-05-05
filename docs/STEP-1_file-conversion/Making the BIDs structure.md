---
title: Making the BIDs structure
nav_order: 2
---

# Making the BIDs structure
The instructions and code here provide the steps needed to anonymize your data and reorganize it into the BIDS specification. It comprises the following **five** steps:

1. [Deidentifying DICOMS](./De-Identifying%20DICOMS.md): Removing identifiable information from file headers using [DicomBrowser](https://download.xnat.org/dicombrowser/)

2. [Converting to NIfTI and BIDS](./Converting%20to%20NIfTI%20and%20BIDS.md): Converting anonymized DICOM files into NIfTI files and reorganizing/renaming files and folders to follow the BIDS specification using [dicm2nii](https://github.com/xiangruili/dicm2nii).

3. Defacing .nii: SNAP anatomical .nii were defaced with pydeface (https://github.com/poldracklab/pydeface).

4. Assembling metadata:
    README 
    dataset_description.json 
    participants.tsv
    participants.json
    task-<>_events.json
    (?) .jsons to supply missing data

5. BIDS Validation: The full PAMD dataset was validated using bids-validator (https://bids-standard.github.io/bids-validator/).

# Preliminary assumptions about data organization
The instructions here make a few assumptions about the organization of data you are starting with. These assumptions can easily be bent, however if you are new to neuroimaging, we recommend establishing the following organization for this project:

```
    studyname
        |-------- data
        |           |-------- sourcedata
        |
        |-------- projects
                    |-------- convert2BIDS        
```

Where `sourcedata` is the folder containing *a copy* of the original files. Needless to say, you should always also keep a pristine copy of your original data stored somewhere other than the computer you're working on. All imaging and related data, including those produced from intermediate and/or analysis steps should go under your `data` folder sorted under appropriately named subfolders. More information about what subfolders you may add to your `data` folder will be described in the relevant instruction sections.

The `projects` folder should be where anything that is not imaging (or related) data goes. Things like analysis scripts, helpful tools that are not installed globally, manuscripts, figures, and anything else useful to the particular project you are working on should be stored under `projects`. The point of this is to create a strong division between the data itself and the tools used to process and summarize data. We recommend creating separate subfolders for each distinct project<sup>[1](#footnotes)</sup>.

We will make reference to this structure and provide further elaborations throughout this document.

## Footnotes
1. *We acknowledge that the `project` folder recommendation differs slightly from the BIDS specification which allows for an optional `code` directory under the `data` folder. For the purpose of working with data, we prefer this organization because it simplifies managing file access permissions and backup policies on multiuser systems where there may be multiple multi-team projects occurring. We have also found it further reinforces the notion of separation of code and data for new users. For archiving purposes, the contents of the project folder can simply be moved to the BIDS recommended `code` folder without any additional changes needed.*
