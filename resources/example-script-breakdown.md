# Script Breakdown

## 1. Prerequisites
Make sure that **Fast CLI** installed globally via npm:
```powershell
npm install --global fast-cli
```
## 2. Create a folder where you want to put the script & CSV files.
```powershell
C:\Speedtest
```
## 3. Delay execution
Adds a short delay to allow the system to stabilize before running the test
```powershell
Start-Sleep -Seconds 20
```
## 4. Define Fast CLI path installed
Points to the location of the fast.ps1 script:
```powershell
$fastPath = "C:\Users\Lee\AppData\Roaming\npm\fast.ps1"
```
## 5. Run Fast CLI and Capture Output
Executes Fast CLI with elevated execution policy and captures JSON output:
```powershell
$jsonText = powershell -ExecutionPolicy Bypass -File $fastPath --upload --latency --json 2>&1 | Out-String
```
## 4. Error Handling
Logs any non-JSON output to an error file:
```powershell
if (-not $jsonText.Trim().StartsWith("{")) {
    $jsonText | Out-File "C:\Speedtest\fast_error.log" -Append
    return
}
```
## 5. Parse JSON and Add Timestamp
Converts JSON output into a PowerShell object and adds a timestamp:
```powershell
$resultJson = $jsonText | ConvertFrom-Json
$DateTime = Get-Date -Format "dd-MM-yyyy HH:mm:ss"
```
## 6. Prepare Data for CSV
Creates a custom object with the relevant speed test information:
```powershell
$data = [PSCustomObject]@{
    DateTime = $DateTime
    Computer = $env:COMPUTERNAME
    Download_Mbps = $resultJson.downloadSpeed
    Upload_Mbps = $resultJson.uploadSpeed
    Latency_ms = $resultJson.latency
}
```
## 7. Export to CSV
Appends the results to a CSV file
```powershell
$csvPath = "C:\Speedtest\speedtest_results.csv"
$data | Export-Csv $csvPath -Append -NoTypeInformation
```
