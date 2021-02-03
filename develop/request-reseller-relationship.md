---
title: Hämta en URL för relationsbegäran
description: Hämta en URL för Relations förfrågan att skicka till en kund.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5f899734b774ff460e005e20df8658275b2ce9d5
ms.sourcegitcommit: d4e652e3b73c6137704d43d4a472cc5aa5549f11
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/09/2020
ms.locfileid: "97770273"
---
# <a name="retrieve-a-relationship-request-url"></a>Hämta en URL för relationsbegäran

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland

Hämta en URL för Relations förfrågan att skicka till en kund.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Om du vill hämta en URL för en Relations förfrågan använder du först [**IAggregatePartner. kunder**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att få ett gränssnitt till partnerns kund åtgärder. Använd sedan egenskapen [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) för att hämta ett gränssnitt till begär ande åtgärder för kund relation. Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) för att hämta URL: en.

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: GetCustomerRelationshipRequest.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                            |
|---------|----------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/relationshiprequests http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inget

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svaret [RelationshipRequest](relationships-resources.md#relationshiprequest) -objektet.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
