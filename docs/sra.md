These guidelines outline the steps for uploading your sequence data (FASTQ files) to NCBI's Sequence Read Archive (SRA) or ENA. All submissions should be associated with our work on the genome of **Biscutella laevigata**. Follow these instructions carefully to ensure your submission is linked to the correct bioproject and that all metadata is complete.

---

## 1. Preparing Your Submission

- **Upload FASTQ Files:**  
  For each dataset, upload the FASTQ files to **NCBI SRA** or **ENA**.
  - If a bioproject already exists, create a new submission and link it to the previous bioproject.
  - If no bioproject exists, create a new one and add all relevant data.
- **Organism Information:**  
  In all metadata templates, ensure that the **organism** field is set to **Biscutella laevigata**.
- See [ena.md](ena.md) for detailed instructions on submitting data to ENA.

---

## 2. Creating the Biosample Sheet for NCBI

A well-prepared biosample sheet is essential for a successful submission. Follow these steps to create a clear and complete biosample sheet:

1. **Download the Template:**
   - In the SRA submission portal, select **Upload file using Excel** to download the biosample sheet template provided by NCBI.

2. **Fill in Mandatory Columns:**
   - **Sample ID:**  
     - Assign a unique identifier for each sample (e.g., `BL_001`, `BL_002`). This will serve as the sample name.
   - **Strain:**  
     - Provide the strain name for the sample. If there are multiple library preps for the same strain, append a suffix (e.g., `-2`, `-3`) to ensure uniqueness.
   - **Bioproject:**  
     - Enter the bioproject ID if available. If creating a new bioproject, you can leave this blank for now.
   - **Organism:**  
     - Enter `Biscutella laevigata`.
   - **Developmental Stage:**  
     - Specify the developmental stage (e.g., `seedling`, `flowering`).
   - **Tissue:**  
     - Specify the tissue type sampled (e.g., `leaf`, `root`, `stem`).

3. **Include Additional Metadata:**
   - **Collected By:**  
     - Enter the name(s) of the person(s) or institution that collected the sample.
   - **Collection Date:**  
     - Provide the date of collection in `YYYY-MM-DD` format.
   - **Latitude/Longitude:**  
     - Combine latitude and longitude into one column using the format:  
       `34.89 S 56.15 W`  
       *(Note: Use the appropriate signs/directions, with North and East being positive.)*

4. **Data Consistency and Formatting:**
   - Ensure that all mandatory columns are filled out for every sample.
   - Avoid spaces or special characters in sample IDs.
   - Verify that the coordinate format is consistent across all entries.

5. **Review and Save:**
   - Double-check the biosample sheet for accuracy.
   - Save the completed file as an Excel or CSV file as per NCBI guidelines.

6. **Upload the Biosample Sheet:**
   - Return to the SRA submission portal and upload the completed biosample sheet.

---

## 3. SRA Metadata Sheet Creation

After completing the biosample sheet, create the SRA metadata sheet as follows:

1. **Download the SRA Metadata Template:**
   - In the SRA portal, choose **Upload file using Excel** to download the metadata sheet template.

2. **Populate Mandatory Fields:**
   - **Sample ID:**  
     - Use the same unique identifier as in the biosample sheet.
   - **Library ID:**  
     - Assign a unique library ID (if not already provided, you can use a similar naming convention as for sample IDs).
   - **Forward and Reverse File Names:**  
     - Fill in the `fq1` and `fq2` columns with the respective FASTQ file names.
   - **Additional Columns:**  
     - Include other required fields such as `title` and `instrument_model`.  
     - Determine the instrument model by referencing the sequencing folder details in the Sequencing Runs Google Sheet.

3. **Save and Upload:**
   - Verify the formatting and save the file as a TSV.
   - Upload the completed metadata sheet to the SRA submission portal.

---

## 4. Pre-upload FASTQ Files Using FTP

1. **Prepare the File List:**
   - Combine the `filename1` and `filename2` columns from your SRA metadata sheet to create a list of files for upload.

2. **FTP Upload Steps:**
   - **Log in to NCBI:**
     - Create (or sign in to) your NCBI account and access the SRA submission portal.
   - **Establish an FTP Connection:**
     ```bash
     ftp ftp-private.ncbi.nlm.nih.gov
     ```
   - **Navigate to Your Account Folder:**
     ```bash
     cd uploads/your_username_submission_folder
     ```
   - **Create a New Folder for the Submission:**
     ```bash
     mkdir 20210121_submission
     ```
   - **Exit the FTP Session:**
     ```bash
     exit
     ```
   - **Upload Files from Terminal (on QUEST):**
     ```bash
     module load parallel
     parallel --verbose lftp -e "put -O /uploads/your_username_submission_folder/20210121_submission {} ; bye" -u subftp,password ftp-private.ncbi.nlm.nih.gov < files_to_upload.tsv
     ```
3. **Important:**  
   Ensure the FTP upload is completely finished before you complete your SRA submission.

---

## 5. Completing the Submission

- **Select the Upload Folder:**
  - In the SRA portal, choose the folder from which you want to pull your files.
- **Review & Submit:**
  - Carefully review all submission details.
  - Submit the data and wait for confirmation; any issues will be reported by the portal.

---

## 6. Current Bioprojects Associated with the Parisod Lab

- **Example Bioproject:**  
  * Biscutella laevigata Genome FASTQ - PRJNA646339  
    [Link to Bioproject](#)

