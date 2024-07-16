---
title: Verificatie
description: Leer hoe u verificatie voor de Adobe Experience Platform Edge Network Server-API configureert.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---

# Verificatie {#authentication}

## Overzicht

[!DNL Edge Network Server API] handelt zowel voor authentiek verklaarde als niet voor authentiek verklaarde gegevensinzameling, afhankelijk van de bron van gebeurtenissen en het API inzamelingsdomein af.

Voor elke aanvraag verifieert [!DNL Server API] de gegevensstroominstelling [!DNL access type] . Met deze instelling kunnen klanten een gegevensstroom configureren voor het accepteren van geverifieerde gegevens of van geverifieerde en niet-geverifieerde gegevens. Standaard worden beide typen gegevens geaccepteerd.

Voor details bij het vormen van het type van datastreamtoegang, zie de documentatie over hoe te [ tot stand brengen en een datastream ](../datastreams/overview.md#create) vormen.

Hieronder volgt een samenvatting van het gedrag, dat op de datastream [!DNL Access Type] configuratie en het eindpunt wordt gebaseerd waarop het verzoek wordt ontvangen.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| gemengd (standaard) | Aanvraag wordt niet geverifieerd | Aanvraag voor verificatie |
| geverifieerd | Aanvraag voor verificatie | Aanvraag voor verificatie |

API-aanroepen die afkomstig zijn van een privéserver op `server.adobedc.net` moeten altijd worden geverifieerd.

## Vereisten {#prerequisites}

Voordat u de methode [!DNL Server API] kunt aanroepen, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een organisatie-account met toegang tot Adobe Experience Platform.
* Voor uw Experience Platform-account zijn de rollen `developer` en `user` ingeschakeld voor het Adobe Experience Platform API-productprofiel. Contacteer uw [ Admin Console ](../access-control/home.md) beheerder om deze rollen voor uw rekening toe te laten.
* Je hebt een Adobe ID. Als u geen Adobe ID hebt, ga naar [ Adobe Developer Console ](https://developer.adobe.com/console) en creeer een nieuwe rekening.

## Referenties verzamelen {#credentials}

Om vraag aan Platform APIs te maken, moet u het [ authentificatieleerprogramma ](../landing/api-authentication.md) eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

De middelen in Experience Platform kunnen aan specifieke virtuele zandbakken worden geïsoleerd. In aanvragen voor platform-API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in Experience Platform, zie de [ documentatie van het zandbakoverzicht ](../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Machtigingen voor schrijven gegevensset configureren {#dataset-write-permissions}

Om dataset te vormen schrijf toestemmingen, ga naar de [ Admin Console ](https://adminconsole.adobe.com), bepaal de plaats van het productprofiel in bijlage aan uw API sleutel, en plaats de volgende toestemmingen:

* Selecteer in de sectie [!UICONTROL Sandboxes] de gegevensstroomsandbox.
* Selecteer in de sectie [!UICONTROL Data Management] de machtiging **[!UICONTROL Manage Datasets]** .

## Problemen met autorisatiefouten oplossen {#troubleshooting-authorization}

| Foutcode | Foutbericht | Beschrijving |
| --- | --- | --- |
| `EXEG-0500-401` | Ongeldig machtigingstoken | Dit foutbericht wordt in een van de volgende situaties weergegeven:  <ul><li>De headerwaarde `authorization` ontbreekt.</li><li>De headerwaarde `authorization` bevat niet de vereiste `Bearer` -token.</li><li>De opgegeven machtigingstoken heeft een ongeldige indeling.</li><li>De gegevensstroom vereist authentificatie maar het verzoek mist vereiste kopballen.</li></ul> |
| `EXEG-0501-401` | Ongeldig token voor gebruikersautorisatie | Dit foutbericht wordt in een van de volgende situaties weergegeven: <ul><li>In de API-aanroep ontbreekt de vereiste `x-user-token` -header.</li><li>De opgegeven gebruikerstoken heeft een ongeldige indeling.</li></ul> |
| `EXEG-0502-401` | Ongeldig machtigingstoken | Dit foutbericht wordt weergegeven wanneer het opgegeven machtigingstoken een geldige indeling (JWT) heeft, maar de handtekening ongeldig is. Controleer het [ authentificatieleerprogramma ](../landing/api-authentication.md) om te leren hoe te om een geldig teken JWT te krijgen. |
| `EXEG-0503-401` | Ongeldig machtigingstoken | Dit foutbericht wordt weergegeven wanneer de opgegeven machtigingstoken is verlopen. Ga door het [ authentificatieleerprogramma ](../landing/api-authentication.md) om een nieuw teken te produceren. |
| `EXEG-0504-401` | Vereiste productcontext ontbreekt | Dit foutbericht wordt in een van de volgende situaties weergegeven:  <ul><li>Het ontwikkelaarsaccount heeft geen toegang tot de Adobe Experience Platform-productcontext.</li><li>Het bedrijfsaccount heeft nog geen recht op een Adobe Experinece Platform.</li></ul> |
| `EXEG-0505-401` | Vereiste tokenbereik van autorisatie ontbreekt | Deze fout is alleen van toepassing op verificatie van serviceaccounts. Het foutbericht wordt weergegeven wanneer het token voor servicevergunning dat in de aanroep is opgenomen, behoort tot een serviceaccount die geen toegang heeft tot het bereik van `acp.foundation` IMS. |
| `EXEG-0506-401` | Sandbox niet toegankelijk voor schrijven | Dit foutbericht wordt weergegeven wanneer de ontwikkelaarsaccount geen `WRITE` toegang heeft tot de Experience Platform-sandbox waarin de gegevensstroom is gedefinieerd. |
