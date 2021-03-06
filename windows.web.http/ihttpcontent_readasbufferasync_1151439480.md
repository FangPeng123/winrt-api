---
-api-id: M:Windows.Web.Http.IHttpContent.ReadAsBufferAsync
-api-type: winrt method
---

<!-- Method syntax
public Windows.Foundation.IAsyncOperationWithProgress<Windows.Storage.Streams.IBuffer, ulong> ReadAsBufferAsync()
-->

# Windows.Web.Http.IHttpContent.ReadAsBufferAsync

## -description
Serialize the HTTP content to a buffer as an asynchronous operation.

## -returns
The object representing the asynchronous operation.

## -remarks
This operation will not block. The returned [IAsyncOperationWithProgress(IBuffer, UInt64)](../windows.foundation/iasyncoperationwithprogress_2.md) object will complete after all of the content has been written to the buffer.

## -examples

## -see-also
[Buffer](../windows.storage.streams/buffer.md)