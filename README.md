<html>

<head>
 <meta name="viewport" content="width=device-width, initial-scale=1" />
</head>


 import requests<br>
import uipath_api_python<br>
Authenticate to UiPath RPA:<br>
 &nbsp;&nbsp;&nbsp;uipath = uipath_api_python.UiPathAPI(
    tenant_logical_name="<TENANT_LOGICAL_NAME>",
    client_id="<CLIENT_ID>",
    client_secret="<CLIENT_SECRET>",
    username="<USERNAME>",
    password="<PASSWORD>")<br>
Get the files from PC or laptop:<br>
def get_files(folder_path):<br>
 &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; 
 &nbsp; &nbsp;   file_list = []<br>
    #by Using requests library to retrieve the list of files from PC or laptop<br>
    response = requests.get("http://<PC_OR_LAPTOP_IP>/files?folder_path=" + folder_path)<br>
   &nbsp; &nbsp; &nbsp;if response.status_code == 200:<br>
    &nbsp;&nbsp;&nbsp;&nbsp; &nbsp;  &nbsp; 
   &nbsp;  &nbsp;   &nbsp; &nbsp;&nbsp;&nbsp;file_list = response.json()<br>
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return file_list<br>
#function is called to retrieve the list of files<br>
files = get_files("C:\MyFiles")<br>
Start a UiPath process to retrieve the files from the memory:<br>
def retrieve_files(file_list):<br>
&nbsp;    #UiPath process to retrieve the files<br>
&nbsp;&nbsp;&nbsp;&nbsp;uipath.start_process("RetrieveFiles", {"files": file_list})<br>
#Calling the function to start the UiPath process<br>
retrieve_files(files)<br>



