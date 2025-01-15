![image](https://github.com/user-attachments/assets/bcaa1fe9-cbd8-4298-aff6-0685d8c9e2cd)# Blob Mover
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

1. When a blob is added or modified (properties only) (V2): 

![image](https://github.com/user-attachments/assets/ff755249-d229-4158-af47-4985f78c6a65)

2. Create file:

![image](https://github.com/user-attachments/assets/4189b08b-18ec-46e5-95df-0d8acc403af0)

Where **File Name** and **File Content** are dynamic content.

# Teams
## What It Does:
Summary of its key components:

1. **Triggers:**
    * The workflow is manually triggered via an HTTP request.

2. **Actions:**
    * The workflow processes alerts from different monitoring services like Resource Health, Service Health, and Activity Log.
    * Depending on the alert's source and severity, it posts messages to a specified Teams channel using Adaptive Cards.
    * The Adaptive Cards include details such as alert title, description, severity, fired time, and other relevant information.
      
3. **Adaptive Cards:**
    * The cards are designed to be visually informative, with sections for images, text blocks, and fact sets.
    * They include actions like opening URLs to Azure Monitor for more details.

4. **Variables:**
    * The workflow initializes variables to store impacted regions and resolved time details.
  
5. **Conditional Logic:**
    * The workflow uses switch cases and conditions to handle different types of alerts and their respective actions.
  
This setup ensures that alerts are communicated effectively to the relevant teams, providing them with all necessary information to respond promptly

## How To Use
Copy the json into the logic app. Update the following two actions to resolved the *Unable to intialise operation* errors when viewed in the Logic App Designer.
1. Create a new action *Post Card in chat or channel* (anywhere) with the required settings i.e. connection, teams channnel (This will be removed later)
   
![image](https://github.com/user-attachments/assets/d1887160-5e83-40d6-a8e4-bfa2064e7641)

![image](https://github.com/user-attachments/assets/c7db7617-a49c-42e5-b00b-6a111a721588)

