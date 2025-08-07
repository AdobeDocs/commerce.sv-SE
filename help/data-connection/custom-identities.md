---
title: Lägg till anpassade attribut till profiler
description: Lär dig hur du lägger till anpassade attribut i kundprofiler.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 5489910382edc70eea5d7c0ca94da41c653b577d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Lägg till anpassade attribut till profiler

Med anpassade profilattribut kan du förbättra identifieringen av kundprofiler i Experience Platform genom att använda ytterligare identifierare utöver standardvärdena `customerId` och `emailId`. Dessa ytterligare identifierare möjliggör exaktare kundmatchning och förbättrad dataintegrering mellan Commerce och Experience Platform.

>[!NOTE]
>
>Lär dig hur du kan [lägga till anpassade attribut](custom-attributes.md) i order.

## Fördelar

- Använd flera identifierare för bättre kundmatchning.
- Mappa anpassade fält till identitetsattribut utifrån ditt företags behov.
- Minska antalet dubblettprofiler och få exaktare kunddata.
- Skapa mer målinriktade kundupplevelser.

## Förutsättningar

Innan du implementerar anpassade identitetsattribut bör du kontrollera att:

- [Installera dataanslutningstillägget](install.md)
- [Anslut till Adobe Experience Platform](connect-data.md)
- [Skicka kundprofildata](connect-data.md#send-customer-profile-data)

## Steg 1: Konfigurera Experience Platform-schema

1. Logga in på Adobe Experience Platform och välj ditt Commerce-schema.
1. [Lägg till anpassade identitetsfält](https://experienceleague.adobe.com/sv/docs/experience-platform/xdm/ui/resources/schemas?lang=en#custom-fields-for-standard-groups) på rotnivå:
   - `hashedPID` (sträng) - hash för primär identitet
   - `hashedSID` (sträng) - hash för sekundär identitet
   - `primaryID` (sträng) - fältnamn för primär identitet
   - `secondaryID` (sträng) - sekundärt ID-fältnamn

![Experience Platform Schema Configuration](./assets/aep-schema-configuration.png)

>[!NOTE]
>
>Du kan anpassa de exakta fältnamnen baserat på dina behov. I exemplet används `hashedPID` och `hashedSID` som identitetsfält.

## Steg 2: Skapa processorklasser

Skapa följande PHP-processorklasser i din anpassade modul:

### Klassen AddressCustomHashedId

Den här processorn hash-kodar `parent_id` och `entity_id` för kundadresser.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['parent_id'] ?? '';
        $sid = $eventData['entity_id'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### Klassen AddressCustomId

Den här processorn anger de primära och sekundära ID-fältnamnen för adresshändelser.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

### Klassen CustomHashedId

Den här processorn hackar `entity_id` och `email` för kundprofiler.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['entity_id'] ?? '';
        $sid = $eventData['email'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### Klassen CustomId

Den här processorn anger de primära och sekundära ID-fältnamnen för profithändelser.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

>[!NOTE]
>Kontrollera att både `primaryID` och `secondaryID` skickas i händelsedata. Om något av dem saknas blir Commerce som standard:
>
>- primär-ID = customerId
>- secondaryID = emailId

>[!BEGINSHADEBOX]

När du har utfört dessa två steg:

- Ditt Commerce-schema i Experience Platform kan importera anpassade identiteter för dina profilhändelsedata.
- Processor-klasser i din Commerce PHP-kod samlar in anpassad identifieringsinformation från profithändelser.

Nu innehåller alla data om profilhändelser som skickas från Commerce din anpassade identifieringsinformation.

>[!ENDSHADEBOX]

## Exempel på dataformat

I följande exempel visas den förväntade JSON-strukturen för anpassade identitetsattribut i både profilattribut och fullständiga dataformat för kundprofiler.

### Profilattributformat

```json
{
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "warehousecode": "1256",
    "method": "ina2354",
    "source": "commerce",
    "primaryID": "hashedPID",
    "secondaryID": "hashedSID"
  }
}
```

### Komplett kundprofilstruktur

```json
{
  "id": 137,
  "entity_id": "137",
  "created_at": "2025-02-10 20:10:30",
  "updated_at": "2022-02-10 20:10:31",
  "email": "customer@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "dob": "2007-10-01 00:00:00",
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "primaryID": "137",
    "secondaryID": "customer@example.com"
  },
  "_metadata": {
    "commerceEdition": "Adobe Commerce",
    "commerceVersion": "2.4.6",
    "eventsClientVersion": "1.9.0",
    "storeId": "1",
    "websiteId": "1",
    "storeGroupId": "1",
    "websiteCode": "base",
    "storeCode": "default",
    "storeViewCode": "main_website_store"
  }
}
```

## Felsökning

### Primärt ID eller sekundärt ID saknas

- **Symptom:** Som standard används data för customerId/emailId i stället för anpassade värden.
- **Lösning:** Kontrollera att både `primaryID` och `secondaryID` har angetts i objektet `profileAttributes`.

### Ogiltiga hash-värden

- **Symtom:** Hash-värden är tomma eller har fel format.
- **Lösning:** Kontrollera att källfälten (`parent_id`, `entity_id`, `email`) innehåller giltiga data innan hash-kodning.

### Processorer körs inte

- **Symptom:** Anpassade attribut visas inte i händelsedata.
- **Lösning:** Kontrollera att processorerna är korrekt registrerade i `events.xml` och att modulen är aktiverad.

### Experience Platform-scheman matchar inte

- **Symptom:** Data visas inte i Experience Platform eller schemavalideringsfel.
- **Lösning:** Kontrollera att Experience Platform-schemat innehåller anpassade identitetsfält med rätt datatyper.
