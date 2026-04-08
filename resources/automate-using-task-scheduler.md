# Windows Task Scheduler
Is a built in feature in Windows where you can automate task such as patching, reporting and etc.

## 1. Open Task Scheduler
Click Create Task
<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/e4301691-9ebe-494b-8bf7-55d03488aa08" />

## 2. General Tab
Fill out the following: 
- **Name**: Hourly Network Test
- **Choose**: Run whether user is logged on or not
- **Check**: Run with highest privileges
<img width="631" height="477" alt="image" src="https://github.com/user-attachments/assets/7f4f234e-8956-47d8-99aa-99ea9e6dfc5f" />

## 3. Triggers Tab
Follow the image below

<img width="594" height="511" alt="image" src="https://github.com/user-attachments/assets/615b5793-15c7-43f6-aaf6-c1ee06af0048" />

## 4. Actions Tab
Fill out the follwing:

- **Action:** Start a program
- **Program/Script:** Locate the powershell.exe file
```powershell
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
  ```
- **Add arguments** (optional):
```powershell
-NoProfile -ExecutionPolicy Bypass -File "C:\NetworkTest\networktest_script.ps1"
```
<img width="459" height="503" alt="image" src="https://github.com/user-attachments/assets/b40998d4-b94a-40e2-90d1-3b1ed78091ba" />

## 5. Conditions Tabs
- **Uncheck:** Start the task only if the computer is on AC power.
<img width="632" height="477" alt="image" src="https://github.com/user-attachments/assets/66d2c837-7368-4ebd-903d-0ce3f203309f" />

## 6. Check the results and errors.
<img width="1918" height="427" alt="image" src="https://github.com/user-attachments/assets/09b19ca3-4ca4-4661-b380-cbf5a255f722" />

**Results**:

<img width="714" height="254" alt="results-csv" src="https://github.com/user-attachments/assets/c28fb7be-5cf4-4a3c-8ff0-37f2b9ecc529" />

Errors:
```powershell
powershell : Please check your internet connection
At C:\NetworkTest\networktest_script.ps1:5 char:13
+ $jsonText = powershell -ExecutionPolicy Bypass -File $fastPath --uplo ...
+             ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (Please check your internet connection:String) [], RemoteException
    + FullyQualifiedErrorId : NativeCommandError

```




