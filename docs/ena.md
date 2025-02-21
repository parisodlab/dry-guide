# Uploading sequence data to ENA

For each project, it is important to also upload the FASTQ files and other raw sequncing files to ENA or SRA (See: __sra.md__) as soon as the sequencing data arrives. **If the study ID already exists, you can create a new sample ID link to the existing study ID**. If there is no previous study ID, you can create a new study ID and add all relevant data. See below for more instructions.

## ENA submission: Important Metadata for DNA and RNA Samples

For plant ecology and evolution studies, providing detailed metadata is crucial. Below are recommended metadata fields:

### Basic Metadata (For Both DNA and RNA)
- **Sample ID:** Unique identifier for each sample.
- **Collection Date:** Date when the sample was collected.
- **Collection Location:** GPS coordinates (latitude and longitude) and a brief description.
- **Collected By:** Name of the person(s) who collected the sample.
- **Species Information:** Scientific name, common name, and additional taxonomic details.
- **Subspecies Information:** Information on subspecies, variety.
- **Population Information:** Details about the population from which the sample originates.
- **Subspecific Genetic Lineage Rank & Name:** Further details on infraspecific classification (e.g., ecotype, cultivar).
- **Altitude:** Altitude of the collection site (in meters).
- **Geographic Location (Region and Locality):** Detailed geographic origin of the sample.
- **Tissue Type:** Type of tissue sampled (e.g., leaf, root, stem).
- **Developmental Stage:** Growth or developmental stage of the organism.
- **Storage Conditions:** How and where the sample was stored (e.g., temperature, preservation method).
- **Extraction Method:** Protocol or kit used for DNA/RNA extraction.
- **Ploidy:** Ploidy level of the genome (e.g., diploid, triploid, tetraploid).
- **Library Preparation:** Details on how the sequencing library was prepared (including kit information).

### Additional Metadata (From the ENA Plant Sample Checklist)
- **Propagation:** Type of reproduction from the parent stock (e.g., sexual/asexual).
- **Soil Classification (FAO):** Soil type based on the FAO World Reference Database for Soil Resources.
- **Soil pH:** pH measurement of the soil at the collection site (e.g., 6.2).
- **Growth Facility:** Type of facility where the plant was grown.
- **Sample Health State:** Overall health status of the subject at the time of collection.
- **Sample Disease Status:** List any diseases diagnosed at the time of collection.
- **Estimated Genome Size:** Estimated size of the genome (in base pairs).
- **Source Material Identifiers:** Unique identifiers assigned to the material sample for traceability, Check the Sample collection list of ParisodLab.

---

### Extended Metadata (Optional but Recommended)

When available, include the following additional fields to capture detailed environmental, collection, and treatment information:

- **Observed Biotic Relationship:** Describe interactions between the subject organism and other organisms (e.g., parasite on species X; mutualist with species Y).
- **Sample Collection Method:** The method employed for collecting the sample (can include a PMID, DOI, URL, or descriptive text).
- **Sample Storage Temperature:** Temperature at which the sample was stored (e.g., -80°C).
- **Sample Storage Location:** Name of the freezer or storage room.
- **Soil Taxonomic / Local Classification:** Local soil classification details.
- **Soil Taxonomic / Local Classification Method:** Reference or method used for local soil classification.
- **Soil Type & Method:** Soil classification using accepted terms (e.g., from ENVO) and the method used.
- **Soil Texture Measurement & Method:** Proportions of sand, silt, and clay (e.g., 40% sand, 30% silt, 30% clay) along with the method used.
- **Sampled Age:** Age of the subject at the time of collection.
- **Sample Disease Stage:** Stage of disease at the time of collection (if applicable).
- **Broad-scale Environmental Context:** Major environmental system of the sample site (e.g., desert, rainforest).
- **Local Environmental Context:** Immediate environmental conditions or influencing entities.
- **Amount or Size of Sample Collected:** Total volume, mass, or area of the sample.
- **Sampling Time Point:** Date/time of collection (ISO 8601 format recommended).
- **Biological Status:** Nature of the sample (e.g., wild, natural, inbred, hybrid).
- **Growth Habit:** General growth form or habit of the plant.
- **Climate, Gaseous, & Seasonal Environment:** Details on the climate, gas concentrations, and season at the time of sampling.
- **Source Material Description:** Additional context clarifying the nature of the source material.
- **Organism Phenotype:** Key phenotypic traits of the organism.
- **Sample Material Processing:** Any processing applied to the sample after collection.
- **Treatment Regimens:**  
  - **Treatment Type:** Type of treatment applied to the sample.
        - **Treatment Duration:** Duration of the treatment.
        - **Treatment Concentration:** Concentration of the treatment.
        - **Treatment Timing:** Timing of the treatment.
        - **Treatment Description:** Detailed description of the treatment.


---

### Sequencing Library Metadata (Mandatory Fields)

For ENA/NCBI submissions, the following sequencing and library metadata fields are **mandatory**:

- **sample:** Unique identifier for the sample.
- **study:** Identifier for the study.
- **instrument_model:** Model of the instrument used for sequencing (permitted values as specified by ENA).
- **library_name:** Name of the sequencing library.
- **library_source:** Source of the library (permitted values).
- **library_selection:** Method used for library selection (permitted values).
- **library_strategy:** Strategy used for library preparation (permitted values).
- **library_layout:** Layout of the library (permitted values).
- **file_name:** File name for reads.
- **file_md5:** MD5 checksum for the file.


### Additional Library Metadata (Optional)
- **library_design:** Details regarding the library design.
- **library_construction_protocol:** Protocol used for library construction.
- **design_description:** Description of the experimental design.
- **insert_size:** Insert size of the library.

---