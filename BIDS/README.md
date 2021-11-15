# Making the BIDs structure
The instructions and code here provide the steps needed to anonymize your data and reorganize it into the BIDS structure. It comprises the following **five** steps:

1. Deidentifying DICOMS: Batch Anonymization of the DICOMS using DicomBrowser https://nrg.wustl.edu/software/dicom-browser/

2. Conversion to .nii and BIDS structure: Anonymized DICOMs were converted to .nii and put into BIDS stucture using dicm2nii (https://github.com/xiangruili/dicm2nii).

3. Defacing .nii: SNAP anatomical .nii were defaced with pydeface (https://github.com/poldracklab/pydeface).

4. Assembling metadata:
    README 
    dataset_description.json 
    participants.tsv
    participants.json
    task-<>_events.json
    (?) .jsons to supply missing data

5. BIDS Validation: The full PAMD dataset was validated using bids-validator (https://bids-standard.github.io/bids-validator/).
