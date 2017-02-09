---
-api-type: winrt method
---
 If no major/minor class of device is set, all devices matching the supplied service capabilities will be returned.
 If no minor class of device is set, all devices matching the major class of devices AND the supplied service capabilities will be returned.
 If service capabilities are set, all devices that match at LEAST the supplied service capabilities AND the major/minor class of device will be returned.
 If no service capabilities are set, all devices that match the major/minor class of device will be returned.
 If no major/minor class of device is set AND no service capabilities are set, all devices will be returned. This AQS Filter string will request an inquiry to be issued.