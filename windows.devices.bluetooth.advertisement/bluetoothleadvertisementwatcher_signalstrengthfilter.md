---
-api-type: winrt property
---
 [InRangeThresholdInDBm](../windows.devices.bluetooth/bluetoothsignalstrengthfilter_inrangethresholdindbm.md) - The maximum value for RSSI for Bluetooth LE is +20. The minimum value for RSSI for BR/EDR is -127 (default when **NULL** is -127.
 [OutOfRangeThresholdInDBm](../windows.devices.bluetooth/bluetoothsignalstrengthfilter_outofrangethresholdindbm.md) - The maximum value for RSSI for Bluetooth LE is +20. The minimum value for RSSI for BR/EDR is -127 (default when **NULL** is -127).
 [OutOfRangeTimeout](../windows.devices.bluetooth/bluetoothsignalstrengthfilter_outofrangetimeout.md) - Equal or greater than 1 second and less than or equal to 60 seconds (default when **NULL** is 60 seconds).
 [SamplingInterval](../windows.devices.bluetooth/bluetoothsignalstrengthfilter_samplinginterval.md) - Equal or greater than 0. Any sampling interval greater or equal to 25.5 seconds will disable sampling entirely. In that special case, the filtering is trigger-based. For more information about the behavior of the RSSI filtering, refer to the [BluetoothSignalStrengthFilter](../windows.devices.bluetooth/bluetoothsignalstrengthfilter.md).