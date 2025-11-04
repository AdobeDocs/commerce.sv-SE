---
title: HIPAA-beredskap för  [!DNL Commerce] tjänster
description: Lär dig hur du kan använda tillägget  [!DNL Data Connection] för att dela [!DNL Commerce] data med Experience Platform och behålla kompatibiliteten med HIPAA.
role: Admin, Leader
feature: Security, Compliance
exl-id: 8851e6d2-c466-4d8e-bfa4-20d0ad6522b5
source-git-commit: 290e3310bd7940c4ccd11317d273b75cc974223b
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# HIPAA-beredskap för [!DNL Commerce]-tjänster

Tillägget [!DNL Data Connection] gör att du kan dela [!DNL Commerce]-data för back office-händelser med Experience Platform och upprätthålla HIPAA-kompatibilitet.

>[!IMPORTANT]
>
>Eftersom butikshändelser genereras på klientsidan är det handlarens ansvar [att inte skicka data för butikshändelser](connect-data.md#data-collection) till Experience Platform.

I den här artikeln får du lära dig:

- Så installerar du
- Hur man säkerställer att data som skickas till Experience Platform är HIPAA-klara
- Datakryptering i [!DNL Commerce]

## Installation

Om du har köpt tillägget för hälsovård för Adobe [!DNL Commerce] har du troligen redan installerat tillägget [HIPAA-Ready](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation). Om du vill vara säker på att dina [!DNL Commerce]-data för back office-händelser är HIPAA-klara måste du även installera [!DNL Data Connection]-tillägget med det extra **Data Services HIPAA**-tillägget. Tillägget **Data Services HIPAA** ser till att alla backoffice-data som du skickar till Experience Platform är HIPAA-klara. Lär dig [installera tillägget](install.md#install-the-data-services-hipaa-extension).

>[!IMPORTANT]
>
>När du installerar tillägget **Data Services HIPAA** hämtas inte längre data för butikshändelser som används av Live Search och produktrekommendationer. Detta beror på att händelsedata för storefront genereras på klientsidan. Om du vill fortsätta att hämta och skicka händelsedata för butiken måste du aktivera händelseinsamlingen för dessa tjänster igen. Mer information finns i [allmän konfiguration](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Hur man säkerställer att data som skickas till Experience Platform är HIPAA-klara

Alla data för back office-händelser som skickas av tillägget [!DNL Data Connection] till Experience Platform anses vara känsliga inom [!DNL Commerce]. Det är emellertid handlarens ansvar att tillämpa dataanvändningsetiketter på sitt [!DNL Commerce]-schema i Experience Platform för att explicit identifiera vissa data som känsliga. När du använder dataanvändningsetiketter direkt på ett schema, sprids dessa etiketter till alla befintliga och framtida datauppsättningar som baseras på det schemat.

En översikt över dataanvändningsetiketter och deras roll i ramverket för datastyrning finns i [översikten över dataanvändningsetiketter](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview) i Experience Platform-dokumentationen.

### Använd dataanvändningsetiketter på [!DNL Commerce] fält

Följ stegen i självstudiekursen [Hantera dataanvändningsetiketter för ett schema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/labels) för att lära dig hur du använder etiketter i ditt [!DNL Commerce]-schema.

Läs [ordlistan med känsliga etiketter](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/reference#sensitive) om du vill veta mer om de tillgängliga etiketterna som du kan använda i fälten i [!DNL Commerce]-schemat. Etiketten `RHD` identifierar till exempel PHI (Protected Health Information) eller information om en patient som Adobe enligt avtal tillåter att du överför.

När dina [!DNL Commerce]-data är märkta som känsliga kan du tillämpa principer för att förhindra dataåtgärder som utgör policyöverträdelser. Läs mer om [policytillämpning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview) i Experience Platform.

## Datakryptering i Commerce

Adobe [!DNL Commerce] använder kryptering på blocknivå. För lagring använder [!DNL Commerce] Amazon Elastic Block Store (EBS). Alla EBS-volymer krypteras med AES-256-algoritmen, vilket innebär att data krypteras i vila. [!DNL Commerce] data som överförs överförs via säkra, krypterade anslutningar med HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

>[!IMPORTANT]
>
>Commerce stöder inte kryptering på kolumn- eller radnivå eller kryptering när data inte finns tillgängliga eller inte är på väg mellan servrar.

### Datakryptering i Experience Platform

När handlare skickar data till Experience Platform skickas dessa med HTTPS TLS v1.2. Läs mer om hur [Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/encryption) krypterar data.

## Hur [!DNL Commerce] hanterar sekretessförfrågningar

Lär dig hur [!DNL Commerce] [hanterar sekretessförfrågningar](handle-privacy-request.md).
