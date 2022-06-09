---
title: Verificatie
description: Leer hoe u verificatie voor de Adobe Experience Platform Edge Network Server API configureert
seo-description: Learn how to configure authentication for the Adobe Experience Platform Edge Network Server API
keywords: gegevensverzameling; authenticatie; Adobe Experience Platform Edge Network api; autorisatie
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 64093bdb8cb1bf2f14caaa562e196a1d69e74359
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# Verificatie {#authentication}

## Overzicht

De [!DNL Edge Network Server API] behandelt zowel voor authentiek verklaarde als niet voor authentiek verklaarde gegevensinzameling, afhankelijk van de bron van gebeurtenissen en het API inzamelingsdomein.

Voor elk verzoek [!DNL Server API] verifieert de datastream [!DNL access type] instellen. Met deze instelling kunnen klanten een gegevensstroom configureren voor het accepteren van geverifieerde gegevens of van geverifieerde en niet-geverifieerde gegevens. Standaard worden beide typen gegevens geaccepteerd.

Voor details bij het vormen van het gegevenstroomtoegangstype, zie de documentatie over hoe te [een gegevensstroom maken en configureren](../edge/datastreams/overview.md#create).

Hieronder volgt een overzicht van het gedrag, gebaseerd op de datastream [!DNL Access Type] configuratie en het eindpunt waarop het verzoek wordt ontvangen.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| gemengd (standaard) | Aanvraag wordt niet geverifieerd | Aanvraag voor verificatie |
| geverifieerd | Aanvraag voor verificatie | Aanvraag voor verificatie |

API-aanroepen die afkomstig zijn van een privéserver op `server.adobedc.net` moet altijd worden geverifieerd.

## Vereisten {#prerequisites}

Alvorens u vraag kunt maken aan [!DNL Server API]moet u aan de volgende voorwaarden voldoen:

* U hebt een IMS-organisatie-account met toegang tot Adobe Experience Platform.
* Je Experience Platform account heeft de `developer` en `user` rollen die zijn ingeschakeld voor het Adobe Experience Platform API-productprofiel. Neem contact op met uw [Admin Console](../access-control/home.md) beheerder om deze rollen voor uw rekening toe te laten.
* Je hebt een Adobe ID. Als je geen Adobe ID hebt, ga dan naar de [Adobe Developer Console](https://developer.adobe.com/console) en maak een nieuwe account.

## Referenties verzamelen {#credentials}

Als u aanroepen wilt uitvoeren naar Platform-API&#39;s, moet u eerst de [verificatiezelfstudie](../landing/api-authentication.md). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

De middelen in Experience Platform kunnen aan specifieke virtuele zandbakken worden geïsoleerd. In aanvragen voor Platform-API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in Experience Platform raadpleegt u de [overzichtsdocumentatie van sandbox](../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Machtigingen voor schrijven gegevensset configureren {#dataset-write-permissions}

Om dataset te vormen schrijf toestemmingen, ga naar [Admin Console](https://adminconsole.adobe.com), zoekt u het productprofiel dat is gekoppeld aan de API-sleutel en stelt u de volgende machtigingen in:

* In de [!UICONTROL Sandboxes] selecteert u de gegevensstroomsandbox.
* In de [!UICONTROL Data Management] selecteert u de **[!UICONTROL Manage Datasets]** toestemming.

## Problemen met autorisatiefouten oplossen {#troubleshooting-authorization}

| Foutcode | Foutbericht | Beschrijving |
| --- | --- | --- |
| `EXEG-0500-401` | Ongeldig machtigingstoken | Dit foutbericht wordt in een van de volgende situaties weergegeven:  <ul><li>De `authorization` koptekstwaarde ontbreekt.</li><li>De `authorization` header value does not include the required `Bearer` token.</li><li>De opgegeven machtigingstoken heeft een ongeldige indeling.</li><li>De gegevensstroom vereist authentificatie maar het verzoek mist vereiste kopballen.</li></ul> |
| `EXEG-0501-401` | Ongeldig token voor gebruikersautorisatie | Dit foutbericht wordt in een van de volgende situaties weergegeven: <ul><li>De API-aanroep ontbreekt `x-user-token` header.</li><li>De opgegeven gebruikerstoken heeft een ongeldige indeling.</li></ul> |
| `EXEG-0502-401` | Ongeldig machtigingstoken | Dit foutbericht wordt weergegeven wanneer het opgegeven machtigingstoken een geldige indeling (JWT) heeft, maar de handtekening ongeldig is. Controleer de [verificatiezelfstudie](../landing/api-authentication.md) om te leren hoe u een geldig JWT-token kunt krijgen. |
| `EXEG-0503-401` | Ongeldig machtigingstoken | Dit foutbericht wordt weergegeven wanneer de opgegeven machtigingstoken is verlopen. Ga door de [verificatiezelfstudie](../landing/api-authentication.md) om een nieuw token te genereren. |
| `EXEG-0504-401` | Vereiste productcontext ontbreekt | Dit foutbericht wordt in een van de volgende situaties weergegeven:  <ul><li>Het ontwikkelaarsaccount heeft geen toegang tot de Adobe Experience Platform-productcontext.</li><li>Het bedrijfsaccount heeft nog geen recht op Adobe Experinece Platform.</li></ul> |
| `EXEG-0505-401` | Vereiste tokenbereik van autorisatie ontbreekt | Deze fout is alleen van toepassing op verificatie van serviceaccounts. Het foutenbericht wordt getoond wanneer het teken van de de dienstvergunning inbegrepen in de vraag tot een de dienstrekening behoort die geen toegang tot heeft `acp.foundation` IMS-bereik. |
| `EXEG-0506-401` | Sandbox niet toegankelijk voor schrijven | Dit foutbericht wordt weergegeven wanneer de ontwikkelaarsaccount niet beschikt over `WRITE` toegang tot de sandbox van het Experience Platform waarin de gegevensstroom is gedefinieerd. |
