# Blob Mover
## What It Does:
Summary of its key components:

1. **Triggers:**
    * **When a blob is added or modified (properties only) (V2)**: This trigger checks for any new or modified blobs in a specified folder every minute.

2. **Actions:**
    * **Get blob content (V2)**: Retrieves the content of the blob that triggered the workflow.
    * **Initialize variable**: Initializes a variable named `filename` with the name of the blob.
    * **Condition** Checks if the blob's filename ends with `.pdf` or `.txt`.
    * **If true:**
      * **Create file**: Creates a file in the `/buscomp` folder with the blob's content.
      * **Get Blob Metadata (V2)**: Retrieves metadata for the blob in the `/successful` folder.
      * **Scope**: Determines whether to rename the blob or not based on its existence in the `/successful` folder.
    * **If false:**
      * **Get Blob Metadata (V2) (copy)**: Retrieves metadata for the blob in the `/failed` folder.
    * **Scope 1**: Similar to the true condition, but for the `/failed` folder.

3. **Final Action:**
    * **Delete blob (V2)**: Deletes the original blob from the `/home` folder after processing.

4. **Connections:**
    * Defines connections to Azure Blob Storage and Azure File Storage.

This workflow essentially monitors a folder for new or modified blobs, processes the blobs based on their file type, and moves them to either a `/successful` or `/failed` folder, while also handling potential renaming conflicts.

## How To Use
Copy the json into the logic app. Update the following two actions to resolved the *Unable to intialise operation* errors when viewed in the Logic App Designer.

* When a blob is added or modified (properties only) (V2): 

![image](https://github.com/user-attachments/assets/ff755249-d229-4158-af47-4985f78c6a65)

* Create file:

![image](https://github.com/user-attachments/assets/4189b08b-18ec-46e5-95df-0d8acc403af0)

Where **File Name** and **File Content** are dynamic content.
