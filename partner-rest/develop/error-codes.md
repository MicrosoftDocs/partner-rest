---
title: Partner API REST error codes
description: Partner REST APIs return a JSON object with a status code about your request's success or failure.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
---

# Partner API REST error codes

Applies to:

- Partner API

Errors in Partner REST APIs are returned using standard HTTP status codes, as well as a JSON error response object.

## HTTP status codes

The following table lists and describes the HTTP status codes that can be returned.

| Status code | Status message                  | Description                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | Bad Request                     | Cannot process the request because it is malformed or incorrect.                                                                       |
| 401         | Unauthorized                    | Required authentication information is either missing or not valid for the resource.                                                   |
| 403         | Forbidden                       | Access is denied to the requested resource. The user might not have enough permission. **Important: if conditional access policies are applied to a resource, `HTTP 403; Forbidden error=insufficent_claims` may be returned.** For more details on Microsoft Graph and conditional access, see [Developer Guidance for Azure Active Directory Conditional Access](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer)  |
| 404         | Not Found                       | The requested resource doesn't exist.                                                                                                  |
| 405         | Method Not Allowed              | The HTTP method in the request is not allowed on the resource.                                                                         |
| 406         | Not Acceptable                  | This service doesn't support the format requested in the Accept header.                                                                |
| 409         | Conflict                        | The current state conflicts with what the request expects. For example, the specified parent folder might not exist.                   |
| 410         | Gone                            | The requested resource is no longer available at the server.                                               |
| 411         | Length Required                 | A Content-Length header is required on the request.                                                                                    |
| 412         | Precondition Failed             | A precondition provided in the request (such as an if-match header) does not match the resource's current state.                       |
| 413         | Request Entity Too Large        | The request size exceeds the maximum limit.                                                                                            |
| 415         | Unsupported Media Type          | The content type of the request is a format that is not supported by the service.                                                      |
| 416         | Requested Range Not Satisfiable | The specified byte range is invalid or unavailable.                                                                                    |
| 422         | Unprocessable Entity            | Cannot process the request because it is semantically incorrect.                                                                        |
| 423         | Locked                          | The resource that is being accessed is locked.                                                                                          |
| 429         | Too Many Requests               | Client application has been throttled and should not attempt to repeat the request until an amount of time has elapsed.                |
| 500         | Internal Server Error           | There was an internal server error while processing the request.                                                                       |
| 501         | Not Implemented                 | The requested feature isn't implemented.                                                                                               |
| 503         | Service Unavailable             | The service is temporarily unavailable for maintenance or is overloaded. You may repeat the request after a delay, the length of which may be specified in a Retry-After header.|
| 504         | Gateway Timeout                 | The server, while acting as a proxy, did not receive a timely response from the upstream server it needed to access in attempting to complete the request. May occur together with 503. |
| 507         | Insufficient Storage            | The maximum storage quota has been reached.                                                                                            |
| 509         | Bandwidth Limit Exceeded        | Your app has been throttled for exceeding the maximum bandwidth cap. Your app can retry the request again after more time has elapsed. |

The error response is a single JSON object that contains a single property
named **error**. This object includes all the details of the error. You can use the information returned here instead of or in addition to the HTTP status code. The following is an example of a full JSON error body.

## Error resource type

The error response is a single JSON object that contains a single property
named **error**. This object includes all the details of the error. You can use the information returned here instead of or in addition to the HTTP status code. The following is an example of a full JSON error body.

The following table and code sample describes the schema of an error
response.

| Name        | Type   | Description                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| code        | string | Always returned. Indicates the kind of error that occurred. Non-null.                          |
| message | string | Always returned. Describes the error in detail, and provides additional debugging information. Non-null, non-empty. Maximum length is 1024 characters. |
| innerError        | object  | Optional. Additional error object that may be more specific than the top level error.                                   |
| target      | string | The target where the error originated.                                                      |

### Code property

The `code` property contains one of the following possible values. Your apps should be
prepared to handle any one of these errors.

| Code                      | Description
|:--------------------------|:--------------
| **accessDenied**          | The caller doesn't have permission to perform the action.
| **generalException**      | An unspecified error has occurred.
| **invalidRequest**        | The request is malformed or incorrect.
| **itemNotFound**          | The resource could not be found.
|**preconditionFailed**     | A precondition provided in the request (such as an if-match header) does not match the resource's current state.
| **resourceModified**      | The resource being updated has changed since the caller last read it, usually an eTag mismatch.
| **serviceNotAvailable**   | The service is not available. Try the request again after a delay. There may be a Retry-After header.
| **unauthenticated**       | The caller is not authenticated.

### Message property

The `message` property at the root contains an error message intended for the
developer to read. Error messages are not localized and shouldn't be displayed
directly to the user. When handling errors, your code should not check against
`message` values because they can change at any time, and they often contain
dynamic information specific to the failed request. You should only code
against error codes returned in `code` properties.

### InnerError object

The `innererror` object might recursively contain more `innererror` objects
with additional, more specific error codes. When handling an error, apps
should loop through all the error codes available and use the most detailed
one that they understand.

There are some additional errors that your app might encounter within the nested
`innererror` objects. Apps are not required to handle these, but can if they
choose. The service might add new error codes or stop returning old ones at any
time, so it is important that all apps be able to handle the [basic error codes]

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```
