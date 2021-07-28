---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform voor 28 juli 2021.
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: ab868a813815e10b520cda2a0abe76e3acdd2ac6
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 28 juli 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Werkruimte voor gegevenswetenschap](#dsw)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Bronnen](#sources)

## Werkruimte voor gegevenswetenschap {#dsw}

De Werkruimte van de Wetenschap van Gegevens gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens tot stand te brengen. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Bibliotheek- en besturingssysteemupdates | De Werkruimte van de Wetenschap van gegevens heeft significante bibliotheek en OS updates gemaakt om functionaliteit en bruikbaarheid te verbeteren. Dit omvat JupyterLab 1.2.20, Python 3.7, Pandas 1.2.4, Tensorflow 2.4.1 met CUDA 11 en CUDNN 8 steun, en meer. Meer informatie over het weergeven van de beschikbare bibliotheken in JupyterLab vindt u in de sectie [Ondersteunde bibliotheken](../../data-science-workspace/jupyterlab/overview.md#supported-libraries) in de documentatie bij het overzicht van JupyterLab-laptops. |

Voor meer algemene informatie over de Werkruimte van de Wetenschap van Gegevens, verwijs naar [Overzicht van de Werkruimte van de Wetenschap van Gegevens](../../data-science-workspace/home.md).

## Doelen {#destinations}

Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| [Sneller bestanden exporteren](../../destinations/ui/activate-destinations.md#export-incremental-files) | U kunt nu incrementele bestandsexporten plannen voor op bestanden gebaseerde doelen om de 3, 6, 8 en 12 uur. Het wijzigen van het schema voor het exporteren van bestanden voor segmenten die al zijn opgeslagen, wordt momenteel niet ondersteund. Om segmenten met een verschillend programma opnieuw uit te voeren, moet u een nieuwe bestemmingsinstantie tot stand brengen. Dit is een beperking die in toekomstige versies zal worden aangepakt. |
| [Ondersteuning voor deduplicatietoetsen](../../destinations/ui/activate-destinations.md#deduplication-keys) | U kunt meerdere records van hetzelfde profiel uit de exportbestanden verwijderen door een deduplicatietoets te selecteren. U kunt één naamruimte of maximaal twee XDM-schemakenmerken selecteren als een deduplicatietoets. |

## Experience Data Model (XDM) {#xdm}

Het Model van Gegevens van de ervaring (XDM) is een open-bronspecificatie die wordt ontworpen om de kracht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor gegevens in de vorm van schema&#39;s, die om het even welke toepassing toestaan om met de diensten van de Platform te communiceren.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Telecommunicatie-industrie, filter | Wanneer het toevoegen van gebiedsgroepen aan een schema in UI, kunt u nu door de telecommunicatiesector filtreren. Zie het [diagram van de de entiteitverhouding van de telecommunicatiesector (ERD)](../../xdm/schema/industries/telecom.md) om een geadviseerd gegevensmodel voor telecomgebruiksgevallen te zien. |

Voor meer algemene informatie over XDM in Platform, verwijs naar [XDM System overview](../../xdm/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] (bèta) | U kunt [!DNL Salesforce Marketing Cloud] nu met Experience Platform verbinden gebruikend [!DNL Flow Service] API of UI. Zie [[!DNL Salesforce Marketing Cloud] connectoroverzicht](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md) voor meer informatie. |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).
