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
