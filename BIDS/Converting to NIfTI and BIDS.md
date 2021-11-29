<img align="right" width="400" src="../docs/images/dcm2nii-and-bids-restructuring/organizing-files.png">

# Converting to NIfTI and BIDS
Converting anonymized DICOM files into NIfTI files and reorganizing/renaming files and folders to follow the BIDS specification.

## Background Information
### The Origins of NIfTI
DICOM images provide a means for storing and sharing a wide variety of medical images. The flexibility provided by the DICOM standard to store many types of images also makes it more difficult to write software to handle the many options available [[1]](#1). Thus, in the early days of neuroimaging there was a need for a file type that would simplify neuroimaging data storage and lower the barrier to software development.

One of the early file types to address this problem was the ANALYZE 7.5 format [[2]](#2). The format was originally developed in the late-1980s as part of a larger software suite aimed at integrating several previously independent and idiosyncratic display algorithms [[3]](#3). The ANALYZE format was designed specifically for multidimensional data (supports up to 7 dimensions)[[2]](#2)[[4]](#4) making it well suited to represent the 4-dimensional volumetric time series common in neuroimaging. It gained widespread use, however contained several critical drawbacks that made working with the file type hazardous. For example, the format split data across two files, a header file (.hdr) and a pixel intensity file (.img). This meant that if one of the files was misplaced,the entire image became unusable.

Of some of the more troublesome problems, ANALYZE 7.5 did not explicitly encode the spatial orientation of the image. This meant that there was no explicit indication as to which part of the image was the participants' left/right, front/back, or top/bottom [[2]](#2)[[5]](#5)[[6]](#6). This turned out to be a crucial flaw of the file format as it sometimes lead to unanticipated left-right flipping of the image so that in was unclear if the experimenter was looking at the participant's left or right side of the brain<sup>[1](#footnotes),[2](#footnotes)</sup>. 

To address the shortcomings of the ANALYZE format, the U.S. National Institutes of Health sponsored a working group called the <u>N</u>euroimaging <u>I</u>n<u>f</u>ormatics <u>T</u>echnology <u>I</u>nitiative<sup>[3](#footnotes)</sup> to create a new neuroimaging data format [[7]](#7). The new format was eponymously called the NIfTI (.nii) format and has become the de facto standard file type for neuroimaging analysis. The first NIfTI standard (NIfTI-1) was developed in 2003 as a modified version of the original ANALYZE 7.5 file type in which unused and optional fields in the header were redefined to address the shortcomings of ANALYZE [[8]](#8). In 2011, the NIfTI committee updated the format to NIfTI-2 in which much of the backwards compatability with ANALYZE was dropped and the allowable size of imaging data expanded [[9]](#9). Currently, NIfTI-1 is still the more common file type [[10]](#10) and the default output of many neuroimaging tools, however both standards are in active use and most major software utilities have agreed to provide support for NIfTI-2 in upcoming releases [[11]](#11). 

NIfTI allows data to be stored as either and .hdr/.img file pair (originally for backwards compatability with non-NIfTI aware software) or as a single *.nii* file [[8]](#8)[[9]](#9). Similar to ANALYZE, NIfTI files can store a series of brain images either as multiple files each containing a single 3D brain volume, or as a single large file in which time is represented along a fourth dimension. The BIDS specification (discussed below) additionally recommends compressing NIfTI files using gzip (thus files with the *.nii.gz* file extension represent one or more compressed *.nii* files<sup>[4](#footnotes)</sup>) [[12]](#12) and are an increasingly common approach to managing the large amounts of data produced by neuroimaging experiments.

### The BIDS Specification
TK

### Footnotes
1. *Note that imaging facilities may use fiducial markers to reduce the potential for left-right errors. These markers, such as a vitamin E capsule taped to one side of the head, will display as a bright mark in the image. It is good practice to be aware of your imaging center's policy for fiduciary marking and to document any marker placement used for your data.*

2. *For a more in-depth discussion of how voxels (*i.e.* volumetric pixels) are mapped onto real-world coordinate systems, take a look at the writings provided by Graham Wideman and Nibabel:*

   + *Orientation and voxel-order terminology ([LINK](www.grahamwideman.com/gw/brain/orientation/orientterms.htm)).*
   + *Coordinate systems and affines ([LINK](https://nipy.org/nibabel/coordinate_systems.html))*
   + *Radiological vs neurological conventions ([LINK](https://nipy.org/neuro_radio_conventions.html))*

3. *The details of the NIfTI format were produced by the Data Format Working Group, a group existing within the larger NIfTI organizational body [[7]](#7).*

4. *Although some neuroimaging tools support working directly with gzipped NIfTI others do not and files must be unzipped prior to use.*

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


  Name					                     Type		    Modality (this will be the output file name)

  AAHead_Scout_64ch_head_coil   	         anat	       HeadScout
  
  t1_mprage_sag_p2_iso                    anat         T1w 
  
  fMRIFieldMap_AP                         anat         FieldMap_AP
  
  fmriFieldMap_PA                         anat         FieldMap_PA
  
  Block_1_SET_SBRef                       func         task-socialevaulation_run-01_sbref
  
  Block_1_SET                             func         task-socialevaulation_run-01_bold
  
  Block_1_RESTING_STATE_SBRef             func         task-resting_run-01_sbref
  
  Block_1_RESTING_STATE                   func         task-resting_run-01_bold
  
  Block1_EGNG_SBRef                       func         tasl-egonogo_run-01_sbref
  
  Block1_EGNG                             func         tasl-egonogo_run-01_bold
  
  AX                                      anat         AX
  
  COR                                     anat         CORT

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

<a id="5">[5]</a>
Wideman, G. (2003, June 22). *Mayo/SPM "analyze" format spec compilation*. Retrieved November 27, 2021, from http://www.grahamwideman.com/gw/brain/analyze/formatdoc.htm.

<a id="6">[6]</a>
Winkler, A. M. (2012, September 23). *The NIFTI file format*. Brainder. Retrieved November 27, 2021, from https://brainder.org/2012/09/23/the-nifti-file-format/. 

<a id="7">[7]</a>
Cox, R. W., Ashburner, J., Breman, H., Fissell, K., Haselgrove, C. Holmes, C. J., Lancaster, J. L., Rex, D. E., Smith, S. M., Woodward, J. B., & Strother, S. C. (2004). *A (sort of) New Image Data Format Standard: NIFTI-1*. Retrieved November 28, 2021, from https://nifti.nimh.nih.gov/nifti-1/documentation/hbm_nifti_2004.pdf.

<a id="8">[8]</a>
Cox, B. (2003). *Breif official definition of the nifti1 header*. National Institute of Mental Health. Retrieved November 28, 2021, from https://nifti.nimh.gov/pub/dist/src/niftilib/nifti1.h

<a id="9">[9]</a>
*NIfTI-2: a 64-bit update of NIfTI1 (approved)*. NITRC. (2011, March 15). Retrieved November 28, 2021, from https://www.nitrc.org/forum/forum.php?thread_id=2148&forum_id=1941.

<a id="10">[10]</a>
NiBabel. (n.d.). *Working with NIfTI images*. Neuroimaging in Python - NiBabel 3.2.1+100.g9fdf5e3e documentation. Retrieved November 28, 2021, from https://nipy.org/nibabel/nifti_images.html.

<a id="11">[11]</a>
Reynolds, R. (2020, April 27). *NIfTI-2 Data Format - Neuroimaging Informatics Technology Initiative*. National Institute of Mental Health. Retrieved November 28, 2021, from https://nifti.nimh.nih.gov/nifti-2.

<a id="12">[12]</a>
*Common Principles -- Imaging files*. Brain Imaging Data Structure v1.6.0. (2021, April 22). Retrieved November 28, 2021, from https://bids-specification.readthedocs.io/en/stable/02-common-principles.html#imaging-files.
