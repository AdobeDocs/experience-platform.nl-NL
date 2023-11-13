---
title: De Reactor-API verifiëren en openen
description: Leer hoe u aan de slag kunt met de Reactor-API, inclusief stappen voor het genereren van de vereiste toegangsreferenties.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# De Reactor-API verifiëren en openen

Voor het gebruik van de [Reactor-API](https://developer.adobe.com/experience-platform-apis/references/reactor/) om de uitbreidingen van Codes tot stand te brengen en te beheren, moet elk verzoek de volgende authentificatiekopballen omvatten:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

In deze handleiding wordt uitgelegd hoe u de Adobe Developer Console kunt gebruiken om de waarden voor elk van deze kopteksten te verzamelen, zodat u aanroepen kunt starten naar de Reactor-API.

## Toegang voor ontwikkelaars tot Adobe Experience Platform {#gain-developer-access}

Voordat u verificatiewaarden voor de Reactor-API kunt genereren, moet u ontwikkelaarstoegang tot het Experience Platform hebben. Volg de eerste stappen in het dialoogvenster [Zelfstudie over verificatie van Experience Platforms](/help/landing/api-authentication.md). Als u de [Toegang van gebruikers verkrijgen](/help/landing/api-authentication.md#gain-user-access) stap terug naar deze zelfstudie om de referenties te genereren die specifiek zijn voor de Reactor-API.

## Toegangsreferenties genereren {#generate-access-credentials}

Met Adobe Developer Console moet u de volgende drie toegangsreferenties genereren:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

De id van uw organisatie (`{ORG_ID}`) en API-sleutel (`{API_KEY}`) kan in toekomstige API-aanroepen opnieuw worden gebruikt nadat deze zijn gegenereerd. Uw toegangstoken (`{ACCESS_TOKEN}`) is tijdelijk en moet om de 24 uur opnieuw worden gegenereerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

### Eenmalige installatie {#one-time-setup}

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die in de zelfstudie worden beschreven [een leeg project maken](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in de documentatie van de Developer Console.

Als u een project hebt gemaakt, selecteert u **API toevoegen** op de **Overzicht van project** scherm.

![](../images/api/getting-started/add-api-button.png)

De **Een API toevoegen** wordt weergegeven. Selecteren **Experience Platform Launch-API** uit de lijst met beschikbare API&#39;s voordat u **Volgende**.

![](../images/api/getting-started/add-launch-api.png)

Selecteer vervolgens het verificatietype dat u wilt maken voor het genereren van toegangstokens en voor toegang tot de Experience Platform-API.

>[!IMPORTANT]
>
>Selecteer de **[!UICONTROL OAuth Server-to-Server]** -methode, aangezien dit de enige methode is die wordt ondersteund om verder te gaan. De **[!UICONTROL Service Account (JWT)]** is vervangen. Terwijl de integratie die de authentificatiemethode JWT gebruikt tot 1 Januari, 2025 zal blijven werken, adviseert de Adobe sterk dat u bestaande integratie aan de nieuwe server-aan-server methode OAuth vóór die datum migreert. Meer informatie ophalen in de sectie [!BADGE Vervangen]{type=negative}[Een JSON-webtoken (JWT) genereren](/help/landing/api-authentication.md#jwt) in de API van het Platform authentificatiezelfstudie.

Selecteren **Volgende** om door te gaan.

![Selecteer de verificatiemethode OAuth Server-to-Server.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

In het volgende scherm wordt u gevraagd een of meer productprofielen te selecteren die u aan de API-integratie wilt koppelen.

>[!NOTE]
>
Productprofielen worden door uw organisatie beheerd via de Adobe Admin Console en bevatten specifieke sets rechten voor korrelfuncties. Productprofielen en hun machtigingen kunnen alleen worden beheerd door gebruikers met beheerdersrechten binnen uw organisatie. Neem contact op met de beheerder als u niet zeker weet welke productprofielen u voor de API moet selecteren.

Selecteer in de lijst de gewenste productprofielen en selecteer vervolgens **geconfigureerde API opslaan** om de API-registratie te voltooien.

![](../images/api/getting-started/select-product-profile.png)

### Referenties verzamelen {#gather-credentials}

Zodra API aan het project is toegevoegd, **[!UICONTROL Experience Platform API]** De pagina voor het project toont de volgende geloofsbrieven die in alle vraag aan Experience Platform APIs worden vereist:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![Integratiegegevens na het toevoegen van een API in de Developer Console.](/help/tags/images/api/getting-started/api-integration-information.png)

### Een toegangstoken genereren {#generate-access-token}

De volgende stap bestaat uit het genereren van een `{ACCESS_TOKEN}` referentie voor gebruik in platform API vraag. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}`moet om de 24 uur een nieuw token worden gegenereerd om door te gaan met het gebruik van platform-API&#39;s.

>[!TIP]
>
Deze tokens verlopen na 24 uur. Als u deze integratie voor een toepassing gebruikt, is het een goed idee om uw token programmatically uit uw toepassing te verkrijgen.

U hebt twee opties om uw toegangstokens te produceren, afhankelijk van uw gebruiksgeval:

* [Tkens handmatig genereren](#manual)
* [Automatisch token genereren](#auto-token)

#### Handmatig toegangstekens genereren {#manual}

Om een nieuwe manueel te produceren `{ACCESS_TOKEN}`, navigeer naar **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** en selecteert u **[!UICONTROL Generate access token]**, zoals hieronder weergegeven.

![Het registreren van het scherm van hoe en toegangstoken in de UI van de Console van de Ontwikkelaar wordt geproduceerd.](/help/tags/images/api/getting-started/generate-access-token.gif)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste koptekst voor autorisatie en moet worden opgegeven in de notatie `Bearer {ACCESS_TOKEN}`.

#### Automatisch token genereren {#auto-token}

U kunt ook een Postman-omgeving en -verzameling gebruiken om toegangstokens te genereren. Lees voor meer informatie de sectie over [het gebruiken van Postman om API vraag voor authentiek te verklaren en te testen](/help/landing/api-authentication.md#use-postman) in de Experience Platform API-verificatiegids.

## API-referenties testen {#test-api-credentials}

Als u de stappen in deze zelfstudie uitvoert, hebt u geldige waarden voor `{ORG_ID}`, `{API_KEY}`, en `{ACCESS_TOKEN}`. U kunt deze waarden nu testen door ze te gebruiken in een eenvoudig cURL-verzoek aan de Reactor-API.

Begin door te proberen een API vraag te maken aan [lijst alle bedrijven](./endpoints/companies.md#list).

>[!NOTE]
>
Mogelijk hebt u geen bedrijven in uw organisatie. In dat geval is de reactie HTTP-status 404 (Niet gevonden). Zolang u geen fout van 403 (Verboden) krijgt, zijn uw toegangsgeloofsbrieven geldig en werkend.

Nadat u hebt bevestigd dat uw toegangsreferenties werken, gaat u verder met de documentatie van de andere API-naslaggids om de vele mogelijkheden van de API te leren kennen.

## API-voorbeeldaanroepen lezen {#read-sample-api-calls}

Elke eindpuntgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/api-guide.md#sample-api) in de gids Aan de slag voor Platform APIs.

## Volgende stappen {#next-steps}

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het richten aan Reactor API. Selecteer een van de eindpunthulplijnen om aan de slag te gaan:

* [Referentiedocumentatie voor Reactor API](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Overzicht van de Reactor-API](/help/tags/api/overview.md)
