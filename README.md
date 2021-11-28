<img align="right" width="200" src="./docs/images/placeholder.png">

# Convert2BIDs


**A step-by-step workflow for converting raw imaging data into anonymized, preprocessed, BIDs-compliant data sets ready for sharing on [OpenNeuro](https://openneuro.org/).**

### Why this Exists
The intent of the resources you will find here is to compile current tools and knowledge on best practices converting raw neuroimaging data into high quality, maintainable, and shareable data sets. Our goal is to lower the barrier to good data keeping practices and increase the number of openly available data sets.

We provide step-by-step instructions and make minimal assumptions about prior knowledge working with imaging data and the associated tools. Where possible, we provide rationales for decision points in this workflow and explanations of the tools and processes employed.

If you find this work useful, find any errors, or discover outdated information, please consider lending your time and knowledge to creating a more robust resource for the neuroimaging community.

*Note that currently this documentation outlines how to prepare a dataset consisting of one or more functional MRI runs, at least one high resolution structural image, and optional field maps.* If we receive feedback that this documentation is helpful, we may add further documentation for preparing other types of scan data. [So let us know what you think!](./discussions)

## Getting Started
Convert2BIDs is divided into **three** major steps. Each of these can be executed independently of each other but often make critical assumptions about the format of the data based on execution of previous steps. It's highly recommended following steps in the order provided. Simply click on each link to be taken to the relevant instruction page.

1. Anonymization, conversion from Dicom to Nifti file formats, and conversion to a BIDs file structure. [(LINK)](BIDS/)
2. Preproccessing
3. Additional quality control and documentation for future analysis
