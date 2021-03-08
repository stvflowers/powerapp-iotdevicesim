# IoT Device Simulator Power App

welcome to the IoT device simulator.

to get started, enter the connection string from your IoT Hub device. it should be formatted like the below:

HostName=<name>.azure-devices.net;DeviceId=<name>;SharedAccessKey=yourSecretKey

Generate a SAS token. it should look like the below:

SharedAccessSignature sr=<name>.azure-devices.net&sig=<secret>&skn=<SAP>

If you are unsure how to generate a SAS token, you can use the IoT Device Explorer or you can use Powershell.
https://docs.microsoft.com/en-us/azure/iot-pnp/howto-use-iot-explorer

```powershell
[Reflection.Assembly]::LoadWithPartialName("System.Web")| out-null
$URI="<your hub name>.servicebus.windows.net/<your endpoint name>"
$Access_Policy_Name="<you SAS policy>"
$Access_Policy_Key="<your SAS policy key>"
#Token expires now+300
$Expires=([DateTimeOffset]::Now.ToUnixTimeSeconds())+300
$SignatureString=[System.Web.HttpUtility]::UrlEncode($URI)+ "`n" + [string]$Expires
$HMAC = New-Object System.Security.Cryptography.HMACSHA256
$HMAC.key = [Text.Encoding]::ASCII.GetBytes($Access_Policy_Key)
$Signature = $HMAC.ComputeHash([Text.Encoding]::ASCII.GetBytes($SignatureString))
$Signature = [Convert]::ToBase64String($Signature)
$SASToken = "SharedAccessSignature sr=" + [System.Web.HttpUtility]::UrlEncode($URI) + "&sig=" + [System.Web.HttpUtility]::UrlEncode($Signature) + "&se=" + $Expires + "&skn=" + $Access_Policy_Name
$SASToken
```

once the stream has started, use the drop down on the right to select a value and an increment. Use the + and - buttons to nudge that attribute while the stream is running. this will help by showing upwards and downwards trends in reports and approaching and triggering alert thresholds.
