<img align="right" width="400" src="../docs/images/dcm2nii-and-bids-restructuring/organizing-files.png">

# Converting to NIfTI and BIDS
Converting anonymized DICOM files into NIfTI files and reorganizing/renaming files and folders to follow the BIDS standard.

## Background Information
DICOM images provide a means for storing and sharing a wide variety of medical images. The flexibility provided by the DICOM standard to store many types of images also makes it more difficult to write software to handle the many options available [[1]](#1). Thus there was a need for an file type that would simplify neuroimaging data storage and lower the barrier to software development.

One of the first file types to address this problem was the ANALYZE 7.5 format.

## Software Setup
TK

## Instructions

1. To open matlab, type "matlab" in home terminal. 
      Once in matlab, using the terminal at the bottom of the window, enter the information below to run dicm2nii converter:
      cd SNAP/Projects/BIDs-Conversion/jillian/dicm2nii-master
      dicm2nii

2. Select the participant's anonymized dicom files ~/STEP/Data/Files from Lab Network Share/AnonDcm/
3. Select output directory: ~/STEP/Data/BIDS/Raw Data/

4. Check presets:
      Output format: BIDS
    Ensure the following are checked:
      Compress
      Left-had storage
      Store PatientName
      #Use parfor if needed
      Use SeriesInstanceUID if exists
      Save json file

5. Click “Start conversion”

6. Check that the following fields are correct:
  Subject: XXXXX (only five-digit participant #)
  Session: Blank
  AcquisitionDate: NaT
  Comment: Blank


  Name					      Type		Modality (this will be the output file name)

  AAHead_Scout_64ch_head_coil   	      anat	      
  t1_mprage_sag_p2_iso                    anat         T1w      
  fMRIFieldMap_AP                         anat  
  fmriFieldMap_PA                         anat
  Block_1_SET_SBRef                       func         task-socialevaulation_run-01_sbref
  Block_1_SET                             func         task-socialevaulation_run-01_bold
  Block_1_RESTING_STATE_SBRef             func         task-resting_run-01_sbref
  Block_1_RESTING_STATE                   func         task-resting_run-01_bold
  Block1_EGNG_SBRef                       func         tasl-egonogo_run-01_sbref
  Block1_EGNG                             func         tasl-egonogo_run-01_bold
  AX                                      anat
  COR                                     anat

*If there are two runs of the same task, check the scan notes to see if the task was repeated. If so change "run-01" to "run-02" for the second run of the task.

7. Hit "ok" and let it run.

## Documentation
TK

## Further Reading
<a id="1">[1]</a>
Li, X., Morgan, P.S., Ashburner, J., Smith, J., & Rorden, C. (2016). The first step for neuroimaging data analysis: DICOM to NIfTI conversion. *Journal of neuroscience methods*, 264, 47-56.
