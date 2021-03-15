# Home UDP Onboarding

This document defines the Home onboarding protocol, this should be used on platforms which do not natively support the HomeKit based onboarding.

## Frames

This header is prefixed in every packet, the serial is a randomly generated number which will be the same
in responses. The length is the length of the entire packet including header, limiting the packet to maximum
size of 64kb, although UDP has a realistic maximum of 2048 bytes. The actual protocol does not accept packets
longer than 512 bytes however.The checksum prevents data corruption and the flags are always one. 
The code indicates what operation is being performed.

Note that references to UUID's are not HomeKit specific, they are the WIFIPLUG UUID system.

```c
{
	char magic[2]; // always 'WP'
	uint16 serial; // randomly generated
	uint16 length; // the length of the entire packet including header
	uint16 checksum; // see below
	uint8 flags; // always 1
	uint8 code; // the code for this packet
} onboard_header (10 bytes);
```

To calculate the checksum, perform the following function on the entire byte array:

```c
for(int i = 0; i < length; i++) {
	checksum += buffer[i];
}
```

## Query All (0x00)

Send via UDP broadcast 8780

```c
{
} onboard_query;
```

## Query by UUID (0x01)

Send via UDP broadcast 8780

```c
{
	char[36] uuid;
} onboard_query;
```

## Query by Mac Address (0x02)

Send via UDP broadcast 8780

```c
{
	char[12] macAddr;
} onboard_query;
```

## Query Response (0x03)

Sent back to UDP client.

```c
{
	uint8 deviceType;
	char[12] macAddr;
	char[36] uuid;
	uint16 flags;
} onboard_queryres;
```

```c
{
	kWifiSetup = 1,
	kHomekitOnboarded = 2,
	kCloudOnboarded = 4,
	kNestOnboarded = 8
} onboard_queryres_flags;
```

## Wifi Setup (0x04)

You can only setup wifi is kWifiSetup flag is not set.
You would usually send this to 192.168.1.100 once the plug's AP has been created.

```c
{
	int8 ssidLen;
	char ssid[ssidLen];
	int8 passLen;
	char pass[passLen];
} onboard_wifi;
```

## Wifi Setup Response (0x05)

This response is sent as the Wifi Setup is underway. A value of kConnected will indicate
the setup is complete and the AP will be promptly closed. The app will have to connect
to wifi network and perform a query to locate the device via MAC and then perform cloud onboard.

```c
{
	int8 stage;
} onboard_wifires;
```

```c
{
	kConnecting = 0,
	kConnected = 1,
	kInvalidSSID = 2,
	kInvalidPassword = 3
} onboard_wifires_stage
```

## Cloud Onboard (0x06)

You can only onboard if kCloudOnboarded flag is not set.

```c
{
	char host[32];
  	int port;
  	char token[48];
} onboard_cloud;
```

## Cloud Onboard Notify (0x07)

This response is sent as the cloud onboarding is underway. The value of kConnected will indicate the setup
is successful

```c
{
	int8 stage;
} onboard_cloudres;
```

```c
{
	kConnecting = 0,
	kInvalidToken = 1,
	kConnected = 2
} onboard_wifires_stage
```

## Identify (0x0A)

Requests the identify routine, e.g flashing like the clappers.

```c
{
} identify_req;
```

## Identify Response (0x0B)

Responds that the identify routine has been completed.

```c
{
} identify_res;
```
