---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Overzicht Microsoft Dynamics Source Connector
description: Leer hoe u Microsoft Dynamics verbindt met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Microsoft Dynamics-connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

[!DNL Experience Platform] biedt ondersteuning voor het opnemen van gegevens van een extern CRM-systeem. Tot de ondersteuning voor CRM-providers behoren [!DNL Microsoft Dynamics] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Veldtoewijzing van [!DNL Microsoft Dynamics] naar XDM

Om een bronverbinding tussen [!DNL Microsoft Dynamics] en Platform tot stand te brengen, moeten de [!DNL Microsoft Dynamics] brongegevensgebieden aan hun aangewezen doelXDM gebieden worden in kaart gebracht alvorens in Platform wordt opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels voor het in kaart brengen van velden tussen [!DNL Microsoft Dynamics] datasets en Platform:

- [Contactpersonen](../adobe-applications/mapping/dynamics.md#contacts)
- [Leads](../adobe-applications/mapping/dynamics.md#leads)
- [Accounts](../adobe-applications/mapping/dynamics.md#accounts)
- [Kansen](../adobe-applications/mapping/dynamics.md#opportunities)
- [Contactrollen opportunity](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campagnes](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Leden van de marketinglijst](../adobe-applications/mapping/dynamics.md#marketing-list-members)

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Microsoft Dynamics] en [!DNL Platform] via API&#39;s of de gebruikersinterface:

## Verbind [!DNL Microsoft Dynamics] met [!DNL Platform] gebruikend APIs

- [Een basisverbinding voor Microsoft Dynamics maken met de Flow Service API](../../tutorials/api/create/crm/ms-dynamics.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een CRM-bron met behulp van de Flow Service API](../../tutorials/api/collect/crm.md)

## Verbind [!DNL Microsoft Dynamics] met [!DNL Platform] gebruikend UI

- [Een Microsoft Dynamics-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/crm/dynamics.md)
- [Een gegevensstroom maken voor een CRM-verbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
