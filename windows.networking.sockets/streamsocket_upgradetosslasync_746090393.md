---
-api-type: winrt method
---
 Create the [StreamSocket](streamsocket.md).
 Get socket control data on a [StreamSocketControl](streamsocketcontrol.md) object using the [Control](streamsocket_control.md) property and set any properties before calling one of the [ConnectAsync](streamsocket_connectasync.md) methods.
 Call one of the [ConnectAsync](streamsocket_connectasync.md) methods to establish a connection with the remote endpoint. If an SSL/TLS connection is required immediately, this can be specified using some of the [ConnectAsync](streamsocket_connectasync.md) methods. If an SSL/TLS connection is desired after sending and receiving some initial data, then the [UpgradeToSslAsync](streamsocket_upgradetosslasync.md) method can be called later to upgrade the connection to use SSL.
 Get the [OutputStream](streamsocket_outputstream.md) property to write data to the remote host.
 Get the [InputStream](streamsocket_inputstream.md) property to read data from the remote host.
 Read and write data as needed.
 Call the [Close](streamsocket_close.md) method to abort any pending operations and release all unmanaged resources associated with the [StreamSocket](streamsocket.md) object.