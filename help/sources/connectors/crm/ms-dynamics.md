---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Overzicht van Microsoft Dynamics Source Connector
topic-legacy: overview
description: Leer hoe u Microsoft Dynamics verbindt met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 4fbf1b9a55c755d0bac9e15efbf6bdb25fa24deb
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Microsoft Dynamics-connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van [!DNL Platform] diensten. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een systeem van derdeCRM. Ondersteuning voor CRM-providers omvat [!DNL Microsoft Dynamics].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Veldtoewijzing van [!DNL Microsoft Dynamics] naar XDM

Een bronverbinding tot stand brengen tussen [!DNL Microsoft Dynamics] en Platform [!DNL Microsoft Dynamics] brongegevensvelden moeten worden toegewezen aan de juiste XDM-doelvelden voordat ze in het Platform worden opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels voor het in kaart brengen van velden tussen [!DNL Microsoft Dynamics] gegevenssets en Platform:

- [Contactpersonen](../adobe-applications/mapping/dynamics.md#contacts)
- [Leads](../adobe-applications/mapping/dynamics.md#leads)
- [Accounts](../adobe-applications/mapping/dynamics.md#accounts)
- [Kansen](../adobe-applications/mapping/dynamics.md#opportunities)
- [Contactrollen opportunity](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campagnes](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Leden van de marketinglijst](../adobe-applications/mapping/dynamics.md#marketing-list-members)

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Microsoft Dynamics] tot [!DNL Platform] API&#39;s of de gebruikersinterface gebruiken:

## Verbinden [!DNL Microsoft Dynamics] tot [!DNL Platform] gebruiken, API&#39;s

- [Een basisverbinding voor Microsoft Dynamics maken met de Flow Service API](../../tutorials/api/create/crm/ms-dynamics.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Creeer een dataflow voor een bron van CRM gebruikend de Dienst API van de Stroom](../../tutorials/api/collect/crm.md)

## Verbinden [!DNL Microsoft Dynamics] tot [!DNL Platform] gebruiken van UI

- [Een Microsoft Dynamics-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/crm/dynamics.md)
- [Een gegevensstroom maken voor een CRM-verbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
