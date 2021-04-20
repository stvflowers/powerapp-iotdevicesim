# IoT Device Simulator Power App

welcome to the IoT device simulator.

to get started, enter the connection string from your IoT Hub device. it should be formatted like the below:

HostName=yourhubname.azure-devices.net;DeviceId=yourdevicename;SharedAccessKey=yourdevicesharedkey

Generate a SAS token. it should look like the below:

SharedAccessSignature sr=yourhubnamehere.azure-devices.net&sig=asecretsignature&skn=yoursharedaccesspolicyname

To generate a SAS token, you can use the Device Explorer:
https://github.com/Azure/azure-iot-sdks/releases/download/2016-11-17/SetupDeviceExplorer.msi

The Connection string should be provided from your IOT HUB DEVICE. It is parsed and the Powerapp/flow builds a connection URL for calling the REST API.

The SAS token is the output from Device Explorer Generate SAS.

Once the stream has started, use the drop down on the right to select a value and an increment. Use the + and - buttons to nudge that attribute while the stream is running. this will help by showing upwards and downwards trends in reports and approaching and triggering alert thresholds.


# Coming Soon
This project will be converted to a code based power app project with Power Fx.
