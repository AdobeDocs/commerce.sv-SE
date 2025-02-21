---
title: Systemkonfigurationsöversikt
description: Lär dig mer om kategorierna med administratörskonfigurationsinställningar som finns för Store-lösningen och hur de är konfigurerade.
role: Admin
feature: Shipping/Delivery, System, Configuration
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Systemkonfigurationsöversikt

I Adobe Commerce Admin kategoriseras konfigurationsinställningarna för Store Fulfillment Services av Walmart Commerce Technologies efter typ.

**Lagra konfigurationsinställningar för uppfyllelse efter typ**

| **Typ** | **Beskrivning** | **API-konfigurerbar** |
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| [Incheckningsmiljön](store-location-map-provider-setup.md) | Konfigurera bilens färg och biltillverkare som ska vara tillgängliga under incheckningsprocessen | Ja |
| [Användarinställningar](user-setup.md) | Hantera användarkonton, roller och behörigheter för butikskopplingar som använder appen Store Assist. omfång. | Ja |
| [Appinställningar](app-setup.md) | Granska tillgängliga konfigurationer för Store Assist App som krävs för att slutföra introduktionsprocessen. Dessa inställningar kan inte konfigureras från Adobe Commerce Admin. | Ja |


## Använd konfigurationsreferensen

Visa konfigurationsreferensen för varje inställningstyp genom att välja typnamnet i tabellen _Store Fulfillment configuration settings by type_.

I konfigurationsreferensen för varje typ visas konfigurationsinformationen i en tabell med följande kolumnrubriker:

- **Fält** refererar till namnet på fältet som ska konfigureras

- **Beskrivning** innehåller viktig information om fältets syfte och beteende

- **Scope** anger Adobe Commerce konfigurationsomfång för inställningen (global, webbplats, butik)

- Värdet **Obligatoriskt** anger om ett värde måste anges för fältet

För tekniska referenser kan du också hitta den interna konfigurationssökvägen för varje fält.

