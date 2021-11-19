<img align="right" width="200" src="../docs/images/DICOM-anonymization/coronal-mprage.png">

# DICOM Anonymization
Removing identifiable information from the DICOM headers. 

## Background Information
Neuroimaging data is typically stored in a file format called DICOM (.dcm) when it is first collected. These follow the [DICOM](https://www.dicomstandard.org) (Digital Imaging and COmmunications in Medice) standard. This is an international formatting standard for medical images. The first part of DICOM files contain a 'header', which contains a variety of metadata about the image, including scan parameters used to acquire the image, information about how the data maps onto real-world-space, and demographic information about the participant [[1]](#1). The second part of the file contains the pixel/voxel intensity information that make up the image.

DICOM header information organizes information by "tags" which are unique numeric identifiers for each piece of information stored. Each piece of information has a four digit "Data Element Number". Similar information is grouped together under a four digit "Group Number". The combined eight-digit number typically displayed in parenthesis, (Group Number followed by Data Element Number), is the "Data Element Tag" that uniquely identifies each piece of information in the header [[2]](#2).

Many tags have, according to the DICOM standard, been reserved for storing specific information. For example, the Data Element Tag (0010, 0010) is called Patient's Name and tag (0008 1030) is called Study Description [[2]](#2). Similar information is often grouped under the same Group Number. For example, Group Number 0010 often contains patient information while Group Number 0008 often contains information about the study, however this is not enforced by the standard [[3]](#3).

While some information is crucial to correctly display the image and should almost never be edited, other data elements constitute identifiable information that must be removed prior to publicly sharing data. Some data like  What counts as identifiable data is constantly evolving as researchers discover new ways to identify individuals with the right pieces of information. For example, 87% of the people in the United States may be identifiable by only their gender, birthdate, and the zip code where they live [[4]](#4). To make matters more confusing, regulatory bodies may use differing criteria. We encourage users of this guide to consult with their supervising ethics boards to ensure compliance in removing all potentially identifiable data.

In the instructions provided below, we provide a list of tags you may want to anonymize. This was based on data collected on MRI machines at the Beckman Institute for Advanced Science and Technology. Your data may differ on what data is stored in the DICOM headers, and you should always thoroughly review the header contents in at least one participant prior to deciding your own anonymization list.

## Software Setup
### *Preliminary Note*
The software setup sections you will encounter throughout this tutorial do not intend to reinvent the wheel and will largely defer to source documentation for installation details. The intent rather is to describe the tools needed for each step (and where to find them).

### Choosing an operating system
Examples used in this tutorial were generated using the Ubuntu 20.04 operating system. We make no specific recommendations regarding computer setup, however keep in mind that some neuroimaging tools (like [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation)) do not run natively on Windows and require additional setup. Command line instructions are specific to the Bash terminal which is part of the default Ubuntu installation.

### DicomBrowser
To anonymize multiple DICOM files at once, we use the DicomBrowser tool ([https://download.xnat.org/dicombrowser/](https://download.xnat.org/dicombrowser/)).

The software can be downloaded as a .deb file which can be installed on the command line with:
```shell
sudo apt install /path/to/filename.deb
```
Replacing the path with the path and filename of the deb file you downloaded. After that, you should be able to open the browser by typing `DicomBrowser` in the terminal.

Although it is possible to use the browser to create scripts to anonymize all dicoms at once, here we describe the interactive method of anonymization.

## Instructions
The following instructions assume the data you have collected (which we will refer to as source data) are grouped by participants with dicoms for individual scans grouped into sub-folders. Subjects may or may not be grouped into further hierarchies such as session, scan site, or cohort as appropriate. So your source data should look something like the following:

```
    sourcedata
        |-------- session_1
                    |-------- subject_1
                    |               |-------- scan_1
                    |               |-------- scan_2
                    |               |-------- scan_3
                    |
                    |-------- subject_2
                    .               |-------- scan_1
                    .               |-------- scan_2
                    .               |-------- scan_3
                
```

1. To start, create a file called AnonDcm in the same directory of your source folder. In the AnonDcm folder, create any subfolders that further organize the subject folders such as session or site.
2. Copy the subject level folder and its contents to the corresponding place in the AnonDcm folder.
3. Open DicomBrowser by typing `DicomBrowser` in the terminal.
4. Click on 'File' and then 'Open', navigate to the folder you intend to anonymize. You can select the entire participant folder and DicomBrowser with search through all subfolders, loading any DICOM files it finds. This allows you to anonymize data for all of a participant's scans at once. 
   1. Depending on the amount of data and computational resources available, this may cause DicomBrowser to hang. If you find this, try loading fewer DICOMs at once, such as going by individual runs.
5. In the left pane, click on the folder that says 'Patient <ID>'. 
   1. This will select all DICOM files that were found with that value in the Patient ID (0010, 0020) tag. If multiple Patient IDs were found (such as if you were anonymizing multiple subjects at once), then they would appear as separate folders in the left panel.

<p align="center" width="100%">
    <img width="100%" src="../docs/images/DICOM-anonymization/DicomBrowser.PNG">
</p>


## 5. Verify that the PatientName/PatientID is the same ID saved in the file name
## 6. Click on the value of the below attributes, alter it to "Anonymous"

+ InstanceCreationDate (0008, 0012)
+ StudyDate (0008, 0020)
+ SeriesDate (0008, 0021)
+ ContentDate (0008, 0023)
+ ReferringPhysicianName (0008, 0090)
+ PerformingPhysicianName (008, 1050)
+ PatientName (0010, 0010)
+ PatientID (0010, 0020)
+ PatientBirthDate (0010, 0030)
+ PatientSize (0010, 1020)
+ PatientWeight (0010, 1030)
+ PatientComments (0010, 4000)
+ Private (0029, 1009)
+ Private (0029, 1019)
+ Private (0029, 1109)
+ Private (0029, 1119)
+ PerformedProcedureStepStartDate (0040,0244)
+ PerformedProcedureStep ID (0040,0253)
## 7. Check that all of the above fields are now "Anonymous"
## 8. Click on "AcquisitionDate - (0008, 0022)" and change to today's date YYYYMMDD 
## 9. Save these DICOMS by "overwriting existing directory."
## 10. Quality Check Step: 

+ Open DicomBrowser by clicking on the icon on your desktop
+ Click on 'File' and then Open, navigate to the folder you intend to check. Under the window "Select DICOM files", click the file so that it is highlighted in blue (not opening it fully) and select "open"
+ Check all fields listed below step number 6 to check that they have been changed to "Anonymous" or a recent date for AcquisitionDate (0008, 0022)
+ While checking the fields listed in step number 6, be sure to check that no additional fields have been changed to anonymous
+ Once you have checked the file, DO NOT SAVE. If everything looks correct, change the corresponding box in the excel sheet green and move to the next file. If there is any issue, make note in the excel sheet and on the slack channel



http://dicomlookup.com/ is a resource which can help find tags.

## Documentation
Here we introduce the documentation system we have found useful for tracking the status of each participant's scans. Proper documentation is crucial component of the pipeline and in this folder, you will find a file called [STUDYNAME_dataprocessing.xlsx](./STUDYNAME_dataprocessing.xlsx) that provides a template with some made up data included for illustration. We will refer to this document throughout this tutorial.

<p align="center" width="100%">
    <img width="100%" src="../docs/images/DICOM-anonymization/study-sheet-dicom-anonymization.JPG">
</p>

Here we have a few example participants undergoing DICOM anonymization. Observe that,

+ Participants are entered according to the data they were scanned and a study identifier. The study identifier is particularly useful for keeping track of multi-session scanning. 
+ Importantly, you will see there is also a place for scan notes. We encourage you to enter brief summaries of information acquired during data collection that may impact analysis decisions. If it is clear from the scan notes that data may be problematic, **do not** just say *excluding*! Instead, write down why this data should not or could not be used. Your future self will thank you. :smiley:
+ The list of IDs are the IDs that you will use in the final BIDS-ified data set. If this does not necessarily need to be the same as the identifiers used when collecting data. If you scroll right in the document, you will find a column at the very end where you can track original IDs.
+ Remember that some of the information you may consider entering (in particular the scan notes and original IDs) may be considered identifiable. *Always carefully review this information before deciding to share publicly.*

DICOM Anonymization occurs in two steps, the anonymization step and the quality control step (see [Instructions](##instructions)). To use this documentation,

1. The person conducting the anonymization should put their initials in the "DICOMS Anonymized column" only for the participants their currently working on. 
2. Once anonymization is complete for a participant, the entry background color should be changed to green to indicate that the data is ready for review.
3. The quality control reviewer should similarly mark their initials in the "DICOM anonymization check" only for participants they are actively reviewing.
4. Tags with any problems should be noted here next to the reviewers initials with a brief explanation of what the problem is. This allows the people doing the anonymization to review and fix these.
5. Once it's been verified that the anonymization was successful and any problems addressed, the "DICOM anonymization check" background color can be changed to green to indicate that the data is ready for the next processing step.

## Further Reading
<a id="1">[1]</a>
Varma, D. R. (2012). Managing DICOM images: Tips and tricks for the radiologist. *The Indian journal of radiology & imaging*, 22(1), 4.

<a id="2">[2]</a>
National Electrical Manufacturers Association (2021) (tech.). *DICOM - Data Dictionary* (Vol. PS3.6, Ser. The DICOM Standard)

<a id="3">[3]</a>
National Electrical Manufacturers Association (2021) (tech.). *DICOM - Message Exchange* (Vol. PS3.7, Ser. The DICOM Standard)

<a id="4">[4]</a>
Sweeney, L. (2000). Simple demographics often identify people uniquely. *Health (San Fransisco)*, *671*(2000), 1-34.