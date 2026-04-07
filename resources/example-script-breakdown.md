# Script Breakdown

## Prerequisites

1. **Fast CLI** installed globally via npm:

```powershell
npm install --global fast-cli
```
2. Create a folder where you want to put the script & CSV files.
```powershell
C:\Speedtest
```
3. Locate the fast.ps1 file. By default it was located in npm folder.
```powershell
$fastPath = "C:\Users\(your username)\AppData\Roaming\npm\fast.ps1"
```
4. Execute Fast CLI with no blockings and captures the data both JSON and non-JSON(errors) format.
```powershell
$jsonText = powershell -ExecutionPolicy Bypass -File $fastPath --upload --latency --json 2>&1 | Out-String
```
5. 
