---
title: Profilposter
description: Lär dig vilka data en profilpost hämtar.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# [!DNL Data Connection] profilposter

Nedan beskrivs de data för profilposter i Commerce som är tillgängliga när du installerar tillägget [!DNL Data Connection]. Data i profilposter skickas till Adobe Experience Platform.

## Profilpost

Profilpostuppdateringar är tillgängliga i Experience Platform när en ny profil skapas, uppdateras eller tas bort.

### Data som samlats in från profilpost

Nedan beskrivs de data som hämtas för en profilpost.

| Fält | Beskrivning |
|---|---|
| `channel` | Innehåller information om datakällan för data. Både `_id` och `_type` innehåller [namnområdesvärden](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/namespaces). |
| `channel._id` | Kanalens unika identifierare, till exempel `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifierar kanaldatakällan, till exempel `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Innehåller information om kunden. |
| `person.name` | Innehåller information om kundens namn. |
| `person.name.firstName` | Innehåller kundens förnamn. |
| `person.name.lastName` | Innehåller kundens efternamn. |
| `person.birthDate` | Köparens födelsedatum. |
| `personalEmail` | En personlig e-postadress. |
| `personalEmail.address` | Den tekniska adressen, till exempel `name@domain.com`, som den är vanlig definierad i RFC2822 och efterföljande standarder. |
| `billingAddress` | Den fakturerande postadressen. |
| `billingAddress.street1` | Primär information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn. |
| `billingAddress.street2` | Ytterligare gatuinformation, andra raden. |
| `billingAddress.city` | Namnet på staden. |
| `billingAddress.state` | Namnet på läget. Det här är ett frihandsfält. |
| `billingAddress.country` | Namnet på det statligt administrerade territoriet. Förutom `xdm:countryCode` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `billingAddress.primary` | Anger om det här är den primära faktureringsadressen. Värdet är alltid `False`. |
| `billingAddressPhone` | Telefonnumret som är associerat med faktureringsadressen. |
| `billingAddressPhone.number` | Telefonnumret. Observera att telefonnumret är en sträng och kan innehålla meningsfulla tecken som hakparenteser `()`, bindestreck `-` eller tecken för att indikera underordnade identifierare som tillägg `x`, till exempel `1-353(0)18391111` eller `+613 9403600x1234`. |
| `billingAddressPhone.primary` | Anger om det här är det primära telefonnumret för faktureringsadressen. Värdet är alltid `False`. |
| `shippingAddress` | Leveransadress. |
| `shippingAddress.street1` | Primär information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn. |
| `shippingAddress.street2` | Ytterligare gatuinformation, andra raden. |
| `shippingAddress.city` | Namnet på staden. |
| `shippingAddress.state` | Namnet på läget. Det här är ett frihandsfält. |
| `shippingAddress.country` | Namnet på det statligt administrerade territoriet. Förutom `xdm:countryCode` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `shippingAddress.primary` | Anger om det här är den primära leveransadressen. Värdet är alltid `False`. |
| `shippingAddressPhone` | Telefonnumret som är associerat med leveransadressen. |
| `shippingAddressPhone.number` | Telefonnumret. Observera att telefonnumret är en sträng och kan innehålla meningsfulla tecken som hakparenteser `()`, bindestreck `-` eller tecken för att indikera underordnade identifierare som tillägg `x`, till exempel `1-353(0)18391111` eller `+613 9403600x1234`. |
| `shippingAddressPhone.primary` | Anger om det här är det primära telefonnumret för leveransadressen. Värdet är alltid `False`. |
| `userAccount` | Anger information om lojalitet, inställningar, inloggningsprocesser och andra kontoinställningar. |
| `userAccount.startDate` | Det datum då profilen skapades för första gången. |

>[!NOTE]
>
>Varje profilpost innehåller även fältet [`identityMap`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/identitymap), som innehåller det systemgenererade Commerce-kund-ID:t som primär identifierare för profilen och ett e-post-ID som används som en sekundär identifierare.

Lär dig hur du [skapar ett profilpostspecifikt schema](profile-data.md) som kan importera data från dina profilposter.
