# Penn-VCC_Methods-Comparison
Information useful for comparing different methods as part of the Penn-Virome Characterization Center as part of the Human Virome Program


## 1. Overview

### Purpose
- The Penn-Virome Characterization Center (Penn-VCC) as part of the Human Virome Program (HVP) is designed to study the virome of healthy individuals across body sites.
- This dataset includes a collection of samples that have undergone several different methods for analyzing the virome of healthy individuals.
- The collection of these samples may be used to determine the potential biases across different methods in identifying viruses across the stool samples. 

### Dataset Organization
- Samples were filtered to have been processed by the most number of different methods. Consequently, all samples are stool samples derived from the IGram cohort from month 01 and month 04 timepoints. By chance, no participant is represented with more than one timepoint.

#### Methods
- 1. Virus-like particle enrichment containing DNA and RNA extraction using reverse transcriptase SSIV and sequenced on a NovaSeq using a 600 cycle kit with paired end 300x300 following Duan VP4 protocol (Processed by the Bushman Lab in 2025/2026)
- 2. Virus-like particle enrichment containing DNA and RNA extraction using reverse transcriptase SSIII and sequenced on a NextSeq using a 300 cycle kit with paired end 150x150 following Duan VP4 protocol (Processed by the Bushman Lab in 2025/2026)
- 3. Virus-like particle enrichment DNA fraction using GenomiPhi V2 amplification sequenced on a HiSeq using a 300 cycle with paired end 150x150 following the Liang et al. protocol (Processed by the Bushman Lab in 2018/2019)
- 4. Virus-like particle enrichment RNA fraction using reverse transcriptase SSIII and polymerase AccuPrime V2 amplification sequenced on a HiSeq using a 300 cycle with paired end 150x150 following the Liang et al. protocol (Processed by the Bushman Lab in 2018/2019)
- 5. Metagenomic Sequencing DNA fraction with no amplification sequenced on a HiSeq using a 300 cycle with paired end 150x150 following the Liang et al. protocol (Processed by the Bushman Lab in 2018/2019)
- 6. Metagenomic Sequencing DNA fraction with no amplification sequenced on a NovaSeq using a 300 cycle with paired end 150x150 following the Moustafa et al. protocol (Processed by the Moustafa Lab in 2025/2026)

Please note: the summary above does not capture all of the intricacies of the different methods, (for example, filtration pore size 0.2um vs 0.8um or different primers used). These differences will change only among different protocols, but all samples within a specified protocol were handled identically. For detailed descriptions of the methods please visit the following references:
- Duan et al., VP 4 Method: PMID: 41278782 https://pubmed.ncbi.nlm.nih.gov/32461640/
- Liang et al., Methods: PMID: 32461640 https://pubmed.ncbi.nlm.nih.gov/41278782/

---

## 2. Sample Hierarchy

### Participant
Variable:
- PVP (Penn Virome Participant)

Description:
- Unique participant identifier.

### Timepoint
Variable:
- timepoint

Description:
- Collection time relative to enrollment or study schedule.

Examples:
- month 01
- month 04 (the majority of samples in this collection)

### Specimen Type
Variable:
- sample_type

Description:
- Biological specimen collected at a specific timepoint.

Examples:
- stool

### Sample Identifier
Variable:
- pt_tp_sp

Description:
- Participant × Timepoint × Specimen combination.
- Represents a unique specimen collection event.

Example:
- PVP1385_month 04_stool

---

## 3. Sequencing Data Structure

### FASTQ File Location
Variable:
- dir_location

Description:
- Full path to FASTQ file on storage.

### FASTQ Filename
Variable:
- file

Description:
- FASTQ filename.

### Read Direction
Variable:
- read

Description:
- Sequencing read orientation.

Possible values:
- R1
- R2

---

## 4. Experimental Variables

### Method
Variable:
- method

Description:
- Description of assay / laboratory workflow.
- May not uniquely define sequencing characteristics.
- Must be interpreted together with run_setup, reverse_transcriptase, polymerase.

Examples:
- metagenomic_dna
- vlp_dna-rna
- ...

### Run Setup
Variable:
- run_setup

Description:
- Sequencing configuration.

Examples:
- novaseq_150_150
- novaseq_300_300
- nextseq_150_150
- ...

Notes:
- A single method may appear under multiple run setups.
- Method and run_setup together define how data were generated.

### Combined Method Definition
Variable:
- method_rt

Description:
- Composite identifier describing assay type, sequencing setup, and reverse transcription conditions.

---

## 5. Sequencing Runs

### Run Identifier
Variable:
- run

Description:
- Sequencing run from which FASTQ files originated.

Examples:
- 20260204_LH00732_0137_B23FT5GLT3

### Relationship to Samples
- One run can contain many samples.
- A sample can potentially appear in multiple runs.
- Technical replicates should be documented here if applicable.

---

## 6. Sample Processing Variables

### Homogenate
Variable:
- homogenate

Description:
- Indicates specimen preparation source.
- Used to differentiate analyses derived from different specimen preparations or tubes.
- For many of the 2025/2026 Bushman and Moustafa Labs samples, these came from tubes that were mixed together, aliquoted, and frozen theoretically avoiding problems of geography of the stool. The Liang et al. processing occured from the same participant timepoint but a different original aliquot that was not originally mixed. 

Possible values:
- 0
- 1
- 2
- ...

Notes:
- Not all methods may originate from the same homogenate.
- Homogenate designation should be considered when comparing methods.

### Reverse Transcription
Variable:
- reverse_transcription

Description:
- Reverse transcription protocol used during library preparation.

Examples:
- none
- SSIII
- SSIV
- ...

### Amplification
Variable:
- amplification

Description:
- Amplification strategy used during library preparation.

Examples:
- none
- AccuPrime
- GenomiPhi_v2

## 7. Known Caveats

- Method criteria alone may not completely describe sequencing characteristics, this should be taken into consideration with the run_setup, reverse_transcriptase, and polymerase variables in additiona to detailed understanding of the individuals protocols described.
- Homogenate differences may introduce variation between assays derived from the same participant/timepoint/specimen.
- Several of the samples from Liang et al., were unclear which timepoint they originated from. A best effort to identify the correct timepoint was made but 1-2 of the samples have ambiguous encoding for the timepoint and could be a participant's stool from a different timepoint.
- Some of the samples are confirmed to be decontaminated (Moustafa Lab processed samples), while others (SRA downloaded samples from Guanxiang et al.) may have had and samples decontaminated with host reads removed by an older version of sunbeam.
- The Exported data for the three methods comparison containing 84 paired samples was trimmed to only contain *_virus_summary.tsv and *_virus.fna files due to issues with file sizes. Directory structure remains unchanged. 

## Data Download
 
[Download Fastq Data for Six Methods Here (Penn+Box Login Required)](https://upenn.box.com/s/o2jmdv125yxm4k4gl3l3rvqqfirxdmcy)
[Download Viral Variant Calls from Six Methods GeNomad Here doi:10.5281/zenodo.21838635](https://doi.org/10.5281/zenodo.21838635)
[Download Viral Variant Calls from Three Methods GeNomad Here (Penn+Box Login Required)](https://upenn.box.com/s/couy37arpds1swc2yz7leudg02jzganl)

