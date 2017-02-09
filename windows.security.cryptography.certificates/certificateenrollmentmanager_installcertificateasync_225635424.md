---
-api-type: winrt method
---
 The certificate request for the input certificate must have been previously generated on the local computer by calling the [CreateRequestAsync](certificateenrollmentmanager_createrequestasync.md) method.
 The certificates included in the response need not be chained to trusted root certificates on the installing computer.
 The certificate is installed in the app container MY store.
 Certification authority (CA) and Root certificates are installed in the app container intermediate CA store.