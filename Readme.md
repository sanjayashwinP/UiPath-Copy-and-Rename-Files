## Exercise_6-UiPath-Copy-and-Rename-Files

## Aim:

To automate the process of copying all files from a source folder to a destination folder and renaming them by appending a timestamp to the file names using UiPath.

## Equipment Required:

UiPath Studio – Installed and ready to create automation workflows.<br>
Computer with:<br>
Minimum 4 GB RAM.<br>
Minimum 2.0 GHz CPU.<br>
Windows operating system.<br>
Source Folder – A folder that contains the files to be copied and renamed.<br>
Destination Folder – A folder where the copied files with the timestamp will be saved.

## Procedure:

### Create a New Process in UiPath Studio:

Open UiPath Studio and click on Process under the New Project tab.<br>
Name the project (e.g., File Copy and Rename Process) and click Create.<br>
This will set up a new automation workflow in which you can define steps to copy and rename files.

### Define Source and Destination Folder Paths:

In the Variables pane, create two string variables:<br>
sourceFolder – This will hold the path of the folder where the original files are stored.<br>
destinationFolder – This will hold the path of the folder where the copied and renamed files will be stored.

### Get List of Files in the Source Folder:

In the Activities panel, search for the Assign activity and drag it into the workflow.<br>
Create a new variable called fileList (Array of Strings) that will hold the list of files from the source folder.<br>
In the Assign activity, set the following expression to get all the file paths from the source folder:<br>

```
fileList = Directory.GetFiles(sourceFolder)
```

This command will retrieve the file paths for all files inside the sourceFolder and store them in the fileList array.

### Loop through Each File in the Source Folder:

In the Activities panel, search for For Each and drag it into the workflow.<br>
Set the Type Argument to String because the file paths will be strings.<br>
In the For Each activity, set the fileList as the Values to iterate over. This will loop through each file path stored in the fileList.

### Copy and Rename Files:

Inside the For Each loop, you will perform multiple actions to copy and rename the files. The steps are as follows:<br>

#### a) Get the File Name:<br>

<br>
Inside the loop, you first need to extract the file name from the file path (e.g., report.pdf).<br>
Use an Assign activity to store the file name in a variable called fileName. Use the following expression:<br>
```
fileName = Path.GetFileName(item)
```
This will extract the file name along with its extension from the file path (e.g., report.pdf from C:\Users\admin\Documents\SourceFolder\report.pdf).<br>

#### b) Append Timestamp to File Name:<br>

<br>
To rename the file, you can append a timestamp to the original file name.<br>
Use an Assign activity to create a new variable called newFileName that will store the renamed file. Use the following expression to append a timestamp:<br>
```
newFileName = Path.GetFileNameWithoutExtension(item) + "_" + Now.ToString("yyyyMMdd_HHmmss") + Path.GetExtension(item)
```
Path.GetFileNameWithoutExtension(item) – Extracts the file name without the extension (e.g., report).<br>
Now.ToString("yyyyMMdd_HHmmss") – Appends the current date and time in the format yyyyMMdd_HHmmss (e.g., 20240926_113045).<br>
Path.GetExtension(item) – Adds the original file extension back (e.g., .pdf).<br>
The final newFileName will look something like report_20240926_113045.pdf, depending on the current date and time.<br>

#### c) Copy the File with the New Name:<br>

<br>
Now that the new file name has been generated, the file can be copied to the destination folder with the renamed file.<br>
Search for the Copy File activity in the Activities panel and drag it into the loop.<br>
In the From property of Copy File, set it to item (the original file path).<br>
In the To property, specify the destination folder and the new file name:<br>
```
destinationFolder + newFileName
```
This will copy the original file from the source folder and rename it with the new name that includes the timestamp, saving it in the destination folder.

### Save and Run the Workflow:

Press CTRL+S to save the workflow.<br>
Click Run to execute the workflow.<br>
The robot will loop through all the files in the source folder, copy each file to the destination folder, and append the timestamp to each file’s name.

## UiPath WorkFlow:

![alt text](<img/Screenshot 2024-09-26 192231.png>)
![alt text](<img/Screenshot 2024-09-26 192316.png>)
![alt text](<img/Screenshot 2024-09-26 192340.png>)
![alt text](<img/Screenshot 2024-09-26 192416.png>)
![alt text](<img/Screenshot 2024-09-26 192512.png>)
![alt text](<img/Screenshot 2024-09-26 192712.png>)
![alt text](<img/Screenshot 2024-09-26 192828.png>)
![alt text](<img/Screenshot 2024-09-26 192912.png>)
![alt text](<img/Screenshot 2024-09-26 192949.png>)

## Result:

After running the UiPath workflow, all files from the source folder are successfully copied to the destination folder and renamed with the current date and time. The timestamps in the file names ensure that files remain unique, and this process can be automated to handle bulk file transfers and renaming efficiently.
