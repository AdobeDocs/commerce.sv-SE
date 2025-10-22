---
title: Hur  [!DNL Commerce] tjänster hanterar sekretessförfrågningar
description: Lär dig hur  [!DNL Commerce] tjänster hanterar begäranden om åtkomst och borttagning av data.
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Sekretessförfrågningar

Adobe Experience Platform Privacy Service tillhandahåller ett RESTful-API och användargränssnitt som hjälper dig att hantera kunddataförfrågningar. Med Privacy Service kan ni skicka in förfrågningar om åtkomst till och radering av personuppgifter från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

Mer information om Privacy Service och hur du skapar och hanterar sekretessförfrågningar finns i Adobe Experience Platform dokumentation:

* [Privacy Service - översikt](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/home)
* [Hantera sekretessjobb i Privacy Service UI](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide)

## Hantera individuella förfrågningar om datasekretess

Du kan skicka enskilda förfrågningar för att få åtkomst till och ta bort konsumentdata från [!DNL Commerce] på två sätt:

* Via **Privacy Service-gränssnittet**. Se dokumentationen [här](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide#_blank).
* Via **Privacy Service API**. Se dokumentationen [här](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank) och API-information [här](https://developer.adobe.com/experience-platform-apis/#_blank).

Privacy Service stöder två typer av förfrågningar: **dataåtkomst** och **dataradering**.

>[!NOTE]
>
>Den här artikeln fokuserar på att göra sekretessförfrågningar för [!DNL Commerce]. Om du planerar att göra sekretessförfrågningar för [Platform data Lake](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/privacy), [Real-Time Customer Profile](https://experienceleague.adobe.com/en/docs/experience-platform/profile/privacy) eller [Identity Service](https://experienceleague.adobe.com/en/docs/experience-platform/identity/privacy), se deras respektive användarhandböcker. Observera att begäranden om borttagning och åtkomst måste göras till varje system för sig, eftersom en sekretessförfrågan till Commerce inte tar bort data från alla dessa system.

## Dataåtkomst

För **åtkomstbegäranden** anger du&quot;Commerce (Personalization)&quot; i användargränssnittet (eller `commerceMarketingData` som produktkod i API:t).

## Borttagning av data

För borttagningsbegäranden tar Privacy Service bort [!DNL Commerce] data som lagras i Commerce SaaS-tjänster för marknadsföringsändamål, vilket innebär att profiler och order för de registrerade inte längre skickas till Adobe marknadsföringsprogram för användning i kampanjer och kundresor. Privacy Service tar dock inte bort data i programmet [!DNL Commerce] eftersom det kan behövas för handelstransaktionsbehov. Handlare ansvarar för alla begäranden om borttagning/åtkomst av data i programmet [!DNL Commerce]. Mer information finns i [Delad ansvarssäkerhet och driftsmodell](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility).

[!DNL Commerce] meddelar handlare om raderingsbegäranden genom att skicka information till dem för registrerade som begär att vissa data ska tas bort.

## Skapa begäranden om åtkomst och borttagning

### Förutsättningar

Om du vill göra förfrågningar om åtkomst och borttagning av data för Adobe [!DNL Commerce] måste du ha:

* ett IMS-organisations-ID
* En identifierare för den person som du vill agera på och motsvarande namnutrymme. Mer information om identitetsnamnutrymmen i Adobe [!DNL Commerce] och Experience Platform finns i [översikten över identitetsnamnrymden](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces).

### Exempel på GDPR-begäran/borttagning av åtkomst:

För **åtkomstbegäranden** anger du&quot;Commerce (Personalization)&quot; i användargränssnittet (eller&quot;commerceMarketingData&quot; som produktkod i API:t).

Kontrollera att kryssrutan Commerce (Personalization) är aktiverad för **borttagningsbegäranden**. Om kundprofil- och orderdata redan har skickats från [!DNL Commerce] till Adobe Experience Platform måste du dessutom skicka borttagningsbegäranden till följande tjänster längre fram i kedjan.

* Profil (produktkod: &quot;profileService&quot;)
* AEP Data Lake (produktkod:&quot;AdobeCloudPlatform&quot;)
* Identitet (produktkod: &quot;identity&quot;)

Om du vill skicka åtkomst- och borttagningsbegäranden via sekretess-API:t måste du autentisera och hantera behörigheter för Privacy Service:

* [Autentisera och få åtkomst till Privacy Service API](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/api/getting-started)
* [Hantera behörigheter för Privacy Service](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/permissions)

**Obligatoriska rubriker**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**Begäran**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**Svar**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
