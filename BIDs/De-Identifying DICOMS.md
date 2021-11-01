# DICOM Anonymization
## 1. Copy files to be anonymized from your raw data folder to the AnonDcm folder 
## 2. Open DicomBrowser by clicking on the icon on your desktop
## 3. Click on 'File' and then Open, navigate to the folder you intend to anonymize. Depending on your computer processing speed, you may either open your DICOMs in the AnonDcm folder and load them here (multiple DICOMs can be chosen at a time) or you can select the entire participant file and load all DICOMs at once. 
## 4. In the left pane, select all subjects
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
