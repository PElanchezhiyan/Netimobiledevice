# Netimobiledevice

Netimobiledevice is a .Net Core implementation for working with all iOS devices (iPhone, iPad, iPod) as well the plists that they use.

- [Netimobiledevice](#Netimobiledevice)
    * [Features](#Features)
    * [Installation](#Installation)
    * [Usage](#Usage)
    * [License](#License)
    * [Contributing](#Contributing)
    * [Acknowledgments](#Acknowledgments)

## Features

 - Device discovery using Usbmux
 - Connect to devices
 - Handling of all Plist types

## Installation

To install Netimobiledevice, you can use the following command in the Package Manager Console:

```powershell
Install-Package Netimobiledevice
```

Alternatively, you can use the .NET CLI:

```csharp
dotnet add package Netimobiledevice
```

# Usage

A few examples of how to use Netimobiledevice are below.

Get a list of all currently connected devices using:

```csharp
using Netimobiledevice.Usbmuxd;

List<UsbmuxdDevice> devices = Usbmux.GetDeviceList();
Console.WriteLine($"There's {devices.Count} devices connected");
foreach (UsbmuxdDevice device in devices) {
    Console.WriteLine($"Device found: {device.DeviceId} - {device.Serial}");
}
```

Listen to connection events:

```csharp
Usbmux.Subscribe(SubscriptionCallback);

private static void SubscriptionCallback(UsbmuxdDevice device, UsbmuxdConnectionEventType connectionEvent)
{
    Console.WriteLine("NewCallbackExecuted");
    Console.WriteLine($"Connection event: {connectionEvent}");
    Console.WriteLine($"Device: {device.DeviceId} - {device.Serial}");
}
```

Get the app icon displayed on the home screen as a PNG:

```csharp
LockdownClient lockdown = new LockdownClient();
SpringBoardServicesService springBoard = new SpringBoardServicesService(lockdown);
PropertyNode png = springBoard.GetIconPNGData("net.whatsapp.WhatsApp");
```

## License

This project is licensed under the [GNU GENERAL PUBLIC LICENSE](https://github.com/artehe/Netimobiledevice/blob/main/LICENSE).

## Contributing

Contributions are welcome. Please submit a pull request or create an issue to discuss your proposed changes.

## Acknowledgments

This library was based on the following repositories with either some refactoring or in the case of libraries such as libusbmuxd translating from C to C#.

- **[BitConverter](https://github.com/davidrea-MS/BitConverter):** Provides a big-endian and little-endian BitConverter that convert base data types to an array of bytes, and an array of bytes to base data types, regardless of machine architecture.
- **[libusbmuxd](https://github.com/libimobiledevice/libusbmuxd):** A client library for applications to handle usbmux protocol connections with iOS devices.
- **[PList-Net](https://github.com/PList-Net/PList-Net):** .Net Library for working with Apple *.plist Files.
- **[pymobiledevice3](https://github.com/doronz88/pymobiledevice3):** A pure python3 implementation to work with iOS devices.
