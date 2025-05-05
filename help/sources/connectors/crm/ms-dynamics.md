---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Overzicht Microsoft Dynamics Source Connector
description: Leer hoe u Microsoft Dynamics met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%

---

# Microsoft Dynamics-connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

[!DNL Experience Platform] biedt ondersteuning voor het opnemen van gegevens van een extern CRM-systeem. Tot de ondersteuning voor CRM-providers behoren [!DNL Microsoft Dynamics] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [&#128279;](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;voor meer informatie.

## Veldtoewijzing van [!DNL Microsoft Dynamics] naar XDM

Als u een bronverbinding wilt maken tussen [!DNL Microsoft Dynamics] en Experience Platform, moeten de [!DNL Microsoft Dynamics] -brongegevensvelden worden toegewezen aan hun juiste doel-XDM-velden voordat ze worden opgenomen in Experience Platform.

Zie het volgende voor meer informatie over de regels voor veldmapping tussen [!DNL Microsoft Dynamics] datasets en Experience Platform:

- [Contactpersonen](../adobe-applications/mapping/dynamics.md#contacts)
- [Leads](../adobe-applications/mapping/dynamics.md#leads)
- [Accounts](../adobe-applications/mapping/dynamics.md#accounts)
- [Kansen](../adobe-applications/mapping/dynamics.md#opportunities)
- [Contactrollen opportunity](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campagnes](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Leden van de marketinglijst](../adobe-applications/mapping/dynamics.md#marketing-list-members)

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Microsoft Dynamics] en [!DNL Experience Platform] via API&#39;s of de gebruikersinterface:

## Verbind [!DNL Microsoft Dynamics] met [!DNL Experience Platform] gebruikend APIs

- [Een Microsoft Dynamics-basisverbinding maken met de Flow Service API](../../tutorials/api/create/crm/ms-dynamics.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een CRM-bron met behulp van de Flow Service API](../../tutorials/api/collect/crm.md)

## Verbind [!DNL Microsoft Dynamics] met [!DNL Experience Platform] gebruikend UI

- [Een Microsoft Dynamics-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/crm/dynamics.md)
- [Een gegevensstroom maken voor een CRM-verbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
