# Data Organization Guidelines

This page outlines how to handle, store, and back up your NGS data so that everyone in the lab has access to well-organized and secure data.

---

## 1. Data Submission

* **Submit Raw Data Promptly:**  
   When you receive raw data from the NGS facility, submit it to either **ENA** or **NCBI**.
   - **Include Metadata:** Attach all necessary metadata.
   - **Set an Embargo:** Apply an embargo if needed, as soon as possible.

* Check out [ENA Guidelines](ena.md) for detailed instructions on how to submit data to ENA.

---

## 2. Data Storage Requirements

* **BigData Server:**
   - Store **raw data** and **final unfiltered results** (e.g., unfiltered VCF files and other outputs) on the BigData server as soon as they are ready.
   - Move **final filtered results** to the BigData server promptly.

* **IBU Account for Long-Term Users:**
   - All long-term users of the Parisod lab should obtain an **IBU account** as soon as possible.
   - **Transfer raw data** to your IBU account.
   - Create and maintain analysis scripts and pipelines, and always use **version control on the ParisodLab GitHub**.

---

## 3. Server Usage Guidelines

### Using p910

#### **Purpose**  
The **p910** server serves **only** as a gateway to access the following UniFR network drives:  

- **BigData**  
- **Common**  
- **OneCopy**  
- Other designated network drives  

#### **Usage Restrictions**  

- **Do not store data long-term** on the `/media/Data` drives.  
- These drives are intended **only** for:  
    - Testing scripts  
    - Temporary storage for short-term users (or those without IBU access)  
    - Managing data transfers between sequencing servers and BigData  

#### **Documentation Management**  

The **p910** server is also used by the system administrator for managing lab documentation, which is version-controlled on the **ParisodLab GitHub**.  

---

## 4. Backup Guidelines on p910

!!! important "Precious Data"
    If you have valuable data that is not considered temporary, please move it to **BigData** as soon as possible.

* **BACKUP Folder (for p910):**
   - A folder named **"BACKUP"** is provided at the base of each drive on the **p910** server.
   - **Important:** Only data stored in this BACKUP folder on p910 will be automatically backed up.
   - Create a subfolder within **BACKUP** with your name and place all critical files there.
   - Organize your data within the subfolder, you should have a clear structure for your data.
   - An **automatic backup script** will copy data from the BACKUP folder to BigData every evening at **5 PM**.
   - We **do not guarantee backups** for any data stored elsewhere.

!!! important "Backup Quota"
    Each user is allowed a maximum backup of **1TB**. You will be notified if you exceed this limit. Keep your data organized and remove unnecessary files to avoid exceeding the limit.  
    If you require additional storage space, please contact the lab administrator.

---

## 5. Key Takeaways

* **Submit raw NGS data** with complete metadata and embargo settings to ENA/NCBI as soon as possible.
* **Ensure metadata** for DNA/RNA samples is detailed and includes:
   - Basic information (population, subspecies, elevation, etc.)
   - Additional fields from the ENA checklist (propagation, soil properties, health status, etc.)
   - Extended metadata when available (environmental context, collection methods, treatment regimens, and sample measurements).
   - **Mandatory sequencing library metadata** (sample, study, instrument model, library details, file names, checksums, and design specifications).

* **Store data on BigData** and use your IBU account for transferring raw data and developing analysis pipelines.
* **Use p910 only to access network drives;** do not store long-term data on the `/media/Data` drives.
* **Back up important data** using the BACKUP folder on p910 to ensure secure, automated backups.
