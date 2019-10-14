### BESC IOT-HUB MQTT INTEGRATION



### Create an IoT Hub

This section describe how to create an IoT Hub using the Azure portal.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Choose **Create a resource**, and then enter *IoT Hub* in the **Search the Marketplace** field.
3. Select **IoT Hub** from the search results, and then select **Create**.
4. On the **Basics** tab, complete the fields as follows:
   - **Subscription**: Select the subscription to use for your hub.
   - **Resource Group**: Select a resource group or create a new one. To create a new one, select **Create new** and fill in the name you want to use. To use an existing resource group, select that resource group. For more information, see [Manage Azure Resource Manager resource groups](https://docs.microsoft.com/en-us/azure/azure-resource-manager/manage-resource-groups-portal).
   - **Region**: Select the region in which you want your hub to be located. Select the location closest to you.
   - **IoT Hub Name**: Enter a name for your hub. This name must be globally unique. If the name you enter is available, a green check mark appears.
5. Select **Next: Size and scale** to continue creating your hub
6. Select **Review + create** to review your choices.
7. Select **Create** to create your new hub. Creating the hub takes a few minutes.

### Register a device

A device must be registered with your IoT Hub before it can connect. Use Azure Cloud Shell to register a device for gateway.

1. Run the following command in Azure Cloud Shell to create device identity.

   **YourIoTHubName**: Replace this placeholder below with the name you chose for your IoT hub.

   **MyNodeDevice**: This is the name of the device you're registering. It's recommended to use **MyNodeDevice** as shown. If you choose a different name for your device, you'll also need to use that name throughout this article, and update the device name in the sample applications before you run them.

```
az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyNodeDevice
```

2. Run the following command in Azure Cloud Shell to get the *device connection string* for the device you just registered:

   **YourIoTHubName**: Replace this placeholder below with the name you chose for your IoT hub.

   ```
   az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyNodeDevice --output table
   ```



### Reference Link

A complete guide of creating IoT Hub using Azure portal and register devices for IoT Hub is available in this link below:

https://docs.microsoft.com/en-us/azure/iot-hub/quickstart-send-telemetry-node



#### Configure Environment File

There is a file named ".env" in the folder, it will be setting for the application

Sample: 

```
CONNECTIONSTRING=HostName=MQTTBESC.azure-devices.net;DeviceId=device1;SharedAccessKey=hKshJEki4vRtQFbmVD6nSvjumi4L7gE0746IT+Fc5YQ=
ENERGY_DATA_PATH=./devicedata.json
REPEAT_EVERY_MINUTES=1
```



Explanation:

|         KEY          |                         DESCRIPTION                          |
| :------------------: | :----------------------------------------------------------: |
|   CONNECTIONSTRING   | A secret **device** connection string provided by Azure IoT Hub to send energy data to cloud. Can be retrieve using Azure CLI. |
|   ENERGY_DATA_PATH   | A file path that are used to locate the devicedata.json file that stores existing energy data. |
| REPEAT_EVERY_MINUTES | Repeat the reading of devicedata.json and data pushing to IoT Hub every n minutes. |



### Starting the application

```
npm install
node server.js
```



Sample Output:

```
Sending message: {
    "Devices": [{
        "name": "Device 4",
        "energy": 112333
        "name": "Device 3",
        "energy": 210.23
    }, {
        "name": "Device 1",
        "energy": 143.32
    }, {
        "name": "Device 2",
        "energy": 34534.2
    }]
}
message sent
```

### NOTE
Run the server sdk https://github.com/epc-blockchain/MQTT-Pull-Azure collect pushed data.




