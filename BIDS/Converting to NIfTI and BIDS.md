<img align="right" width="400" src="../docs/images/dcm2nii-and-bids-restructuring/organizing-files.png">

# Converting to NIfTI and BIDS
Converting anonymized DICOM files into NIfTI files and reorganizing/renaming files and folders to follow the BIDS standard.

## Background Information
DICOM images provide a means for storing and sharing a wide variety of medical images. The flexibility provided by the DICOM standard to store many types of images also makes it more difficult to write software to handle the many options available [[1]](#1). Thus, in the early days of neuroimaging there was a need for a file type that would simplify neuroimaging data storage and lower the barrier to software development.

One of the early file types to address this problem was the ANALYZE 7.5 format [[2]](#2). The format was originally developed in the late-1980s as part of a larger software suite aimed at integrating several previously independent and idiosyncratic display algorithms [[3]](#3). The ANALYZE format was designed specifically for multidimensional data (supports up to 7 dimensions)[[2]](#2)[[4]](#4) making it well suited to represent the 4-dimensional volumetric time series common in neuroimaging. It gained widespread use, however contained several critical drawbacks that made working with the file type hazardous. For example, the format split data across two files, a header file (.hdr) and the pixel intensity file (.img). Of some of the more troublesome problems, ANALYZE 7.5 did not explicitly encode orientation of the 

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

<a id="2">[2]</a>
Larobina, M., & Murino, L. (2014). Medical image file formats. *Journal of digital imaging*. *27*(2), 200-206.

<a id="3">[3]</a>
Robb, R.A., Hanson, D.P., Karwoski, R.A., Larson, A.G., Workman, E.L., & Stacy, M.C. (1989). Analyze: A comprehensive, operator-interactive software package for multidimensional medical image display and analysis. *Computerized Medical Imaging and Graphics*, *13*(6), 433-454.

<a id="4">[4]</a>
Cox, B. (2019, March). *File nifti1.h -- Brief official definition of the nifti1 header*. National Institute of Mental Health. Retrieved November 23, 2021, from https://nifti.nimh.nih.gov/pub/dist/src/niftilib/nifti.h.