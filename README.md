# IoT Device Simulator Power App

welcome to the IoT device simulator.

to get started, enter the connection string from your IoT Hub device. it should be formatted like the below:

HostName=yourhubname.azure-devices.net;DeviceId=yourdevicename;SharedAccessKey=yourdevicesharedkey

Generate a SAS token. it should look like the below:

SharedAccessSignature sr=yourhubnamehere.azure-devices.net&sig=asecretsignature&skn=yoursharedaccesspolicyname

If you are unsure how to generate a SAS token, you can use the IoT Device Explorer or you can use Powershell.
https://docs.microsoft.com/en-us/azure/iot-pnp/howto-use-iot-explorer


```powershell
######
## Edit the variables to match your information
##

$namespace = "" #IoT Hub
$endpoint = "" #IoT Hub Device connection string. Must include SAS policy name and key
$SASpolicyName = "" #IoT Hub SAS policy
$SASpolicyKey = "" #IoT Hub SAS policy key
$tokenExpiry = 300 #Token validity time in seconds


[Reflection.Assembly]::LoadWithPartialName("System.Web")| out-null
$URI="$namespace.servicebus.windows.net/$endpoint"
$Access_Policy_Name=$SASpolicyName
$Access_Policy_Key=$SASpolicyKey
$Expires=([DateTimeOffset]::Now.ToUnixTimeSeconds())+$tokenExpiry
$SignatureString=[System.Web.HttpUtility]::UrlEncode($URI)+ "`n" + [string]$Expires
$HMAC = New-Object System.Security.Cryptography.HMACSHA256
$HMAC.key = [Text.Encoding]::ASCII.GetBytes($Access_Policy_Key)
$Signature = $HMAC.ComputeHash([Text.Encoding]::ASCII.GetBytes($SignatureString))
$Signature = [Convert]::ToBase64String($Signature)
$SASToken = "SharedAccessSignature sr=" + [System.Web.HttpUtility]::UrlEncode($URI) + "&sig=" + [System.Web.HttpUtility]::UrlEncode($Signature) + "&se=" + $Expires + "&skn=" + $Access_Policy_Name
$SASToken

```

The Connection string should be provided from your IOT HUB DEVICE. It is parsed and the Powerapp/flow builds a connection URL for calling the REST API.

The SAS string should be the SAS of your IOT HUB NAMESPACE. It is used to request a token based on a SAS POLICY. This SAS policy and TOKEN is what grants you access to the device to send messages to.

once the stream has started, use the drop down on the right to select a value and an increment. Use the + and - buttons to nudge that attribute while the stream is running. this will help by showing upwards and downwards trends in reports and approaching and triggering alert thresholds.


# Coming Soon
This project will be converted to a code based power app project with Power Fx.
