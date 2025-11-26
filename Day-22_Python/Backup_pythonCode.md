# Created code to take backup of the folder in python code using function
```
import shutil
import datetime
import os

def backup_files(source, destination):
    today = datetime.date.today()
    backup_files_name = os.path.join(destination, f"backup_{today}.zip")
    shutil.make_archive(backup_files_name.replace('zip',''),'zip',source)


source = "c:/Users/111685/OneDrive - Arrow Electronics, Inc/Study Material/Devops Study/Python"
destination = "c:/Users/111685/OneDrive - Arrow Electronics, Inc/Study Material/Devops Study/Python/backup"
backup_files(source,destination)

```
------------
source = "c:/Users/111685/OneDrive - Arrow Electronics, Inc/Study Material/Devops Study/Python"
destination = "c:/Users/111685/OneDrive - Arrow Electronics, Inc/Study Material/Devops Study/Python/backup"
backup_files(source,destination)
## Tested the code 
<img width="1279" height="560" alt="image" src="https://github.com/user-attachments/assets/3db13730-482c-4da8-bbf7-3f915d500013" />

--------
