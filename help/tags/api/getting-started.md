---
title: De Reactor-API verifiëren en openen
description: Leer hoe u aan de slag kunt met de Reactor-API, inclusief stappen voor het genereren van de vereiste toegangsreferenties.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# De Reactor-API verifiëren en openen

Om [ Reactor API ](https://developer.adobe.com/experience-platform-apis/references/reactor/) te gebruiken om de uitbreidingen van Codes tot stand te brengen en te beheren, moet elk verzoek de volgende authentificatiekopballen omvatten:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

In deze handleiding wordt uitgelegd hoe u de Adobe Developer Console kunt gebruiken om de waarden voor elk van deze kopteksten te verzamelen, zodat u aanroepen kunt starten naar de Reactor-API.

## Toegang voor ontwikkelaars tot Adobe Experience Platform {#gain-developer-access}

Voordat u verificatiewaarden voor de Reactor-API kunt genereren, moet u toegang voor ontwikkelaars tot Experience Platform hebben. Om ontwikkelaartoegang te verkrijgen, volg de eerste stappen in het [ de authentificatieleerprogramma van Experience Platform ](/help/landing/api-authentication.md). Zodra u de [ stap van de Toegang van de Gebruiker van de Versterking ](/help/landing/api-authentication.md#gain-user-access) hebt voltooid, terugkeer naar dit leerprogramma om de geloofsbrieven te produceren specifiek voor Reactor API.

## Toegangsreferenties genereren {#generate-access-credentials}

Met Adobe Developer Console moet u de volgende drie toegangsreferenties genereren:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Identiteitskaart van uw organisatie (`{ORG_ID}`) en de sleutel van API (`{API_KEY}`) kunnen in toekomstige API vraag worden opnieuw gebruikt nadat zij aanvankelijk zijn geproduceerd. Nochtans, is uw toegangstoken (`{ACCESS_TOKEN}`) tijdelijk en moet om de 24 uur worden opnieuw geproduceerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

### Eenmalige installatie {#one-time-setup}

Ga naar [ Adobe Developer Console ](https://www.adobe.com/go/devs_console_ui) en teken binnen met uw Adobe ID. Daarna, volg de stappen die in het leerprogramma worden geschetst op [ creërend een leeg project ](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in de documentatie van Developer Console.

Zodra u een project hebt gecreeerd, uitgezocht **voeg API** op het **Overzicht van het Project** scherm toe.

![](../images/api/getting-started/add-api-button.png)

**voeg API** scherm toe verschijnt. Selecteer **de Lanceer API van het Platform van de Ervaring** van de lijst van beschikbare APIs alvorens **daarna** te selecteren.

![](../images/api/getting-started/add-launch-api.png)

Selecteer vervolgens het verificatietype dat u wilt genereren voor toegangstokens en toegang tot de Experience Platform API.

>[!IMPORTANT]
>
>Selecteer de methode **[!UICONTROL OAuth Server-to-Server]** omdat dit de enige methode is die u kunt gebruiken om door te gaan. De methode **[!UICONTROL Service Account (JWT)]** is vervangen. Terwijl de integratie die de authentificatiemethode JWT gebruikt tot 1 Januari, 2025 zal blijven werken, adviseert Adobe sterk dat u bestaande integratie aan de nieuwe server-aan-server methode OAuth vóór die datum migreert. Krijg meer informatie in de sectie [!BADGE  Afgekeurd ]{type=negative}[ produceer een Token van het Web JSON (JWT) ](/help/landing/api-authentication.md#jwt) in het de authentificatieleerprogramma van Experience Platform API.

Selecteer **daarna** om verder te gaan.

![ Uitgezochte Server-aan-Server authentificatiemethode.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

In het volgende scherm wordt u gevraagd een of meer productprofielen te selecteren die u aan de API-integratie wilt koppelen.

>[!NOTE]
>
Productprofielen worden door uw organisatie beheerd via de Adobe Admin Console en bevatten specifieke sets rechten voor korrelfuncties. Productprofielen en hun machtigingen kunnen alleen worden beheerd door gebruikers met beheerdersrechten binnen uw organisatie. Neem contact op met de beheerder als u niet zeker weet welke productprofielen u voor de API moet selecteren.

Selecteer de gewenste productprofielen van de lijst, dan uitgezocht **sparen gevormde API** om de API registratie te voltooien.

![](../images/api/getting-started/select-product-profile.png)

### Referenties verzamelen {#gather-credentials}

Zodra API aan het project is toegevoegd, **[!UICONTROL Experience Platform API]** toont de pagina voor het project de volgende geloofsbrieven die in alle vraag aan Experience Platform APIs worden vereist:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![ de informatie van de Integratie na het toevoegen van API in Developer Console.](/help/tags/images/api/getting-started/api-integration-information.png)

### Een toegangstoken genereren {#generate-access-token}

De volgende stap bestaat uit het genereren van een `{ACCESS_TOKEN}` -referentie voor gebruik in Experience Platform API-aanroepen. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}` , moet om de 24 uur een nieuw token worden gegenereerd om Experience Platform API&#39;s te kunnen blijven gebruiken.

>[!TIP]
>
Deze tokens verlopen na 24 uur. Als u deze integratie voor een toepassing gebruikt, is het een goed idee om uw token programmatically uit uw toepassing te verkrijgen.

U hebt twee opties om uw toegangstokens te produceren, afhankelijk van uw gebruiksgeval:

* [Tkens handmatig genereren](#manual)
* [Automatisch token genereren](#auto-token)

#### Handmatig toegangstekens genereren {#manual}

Als u handmatig een nieuwe `{ACCESS_TOKEN}` wilt genereren, navigeert u naar **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** en selecteert u **[!UICONTROL Generate access token]** (zie hieronder).

![ opname van het Scherm van hoe en toegangstoken in Developer Console UI wordt geproduceerd.](/help/tags/images/api/getting-started/generate-access-token.gif)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste machtigingsheader en moet worden opgegeven in de indeling `Bearer {ACCESS_TOKEN}` .

#### Automatisch token genereren {#auto-token}

U kunt ook een Postman-omgeving en -verzameling gebruiken om toegangstokens te genereren. Voor meer informatie, lees de sectie over [ gebruikend Postman om API vraag ](/help/landing/api-authentication.md#use-postman) in de de authentificatiegids van Experience Platform voor authentiek te verklaren en te testen API.

## API-referenties testen {#test-api-credentials}

Door de stappen in deze zelfstudie uit te voeren, hebt u geldige waarden voor `{ORG_ID}`, `{API_KEY}` en `{ACCESS_TOKEN}` . U kunt deze waarden nu testen door ze te gebruiken in een eenvoudig cURL-verzoek aan de Reactor-API.

Begin door te proberen om een API vraag te maken aan [ lijst alle bedrijven ](./endpoints/companies.md#list).

>[!NOTE]
>
Mogelijk hebt u geen bedrijven in uw organisatie. In dat geval is de reactie HTTP-status 404 (Niet gevonden). Zolang u geen fout van 403 (Verboden) krijgt, zijn uw toegangsgeloofsbrieven geldig en werkend.

Nadat u hebt bevestigd dat uw toegangsreferenties werken, gaat u verder met de documentatie van de andere API-naslaggids om de vele mogelijkheden van de API te leren kennen.

## API-voorbeeldaanroepen lezen {#read-sample-api-calls}

Elke eindpuntgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/api-guide.md#sample-api) in de begonnen gids voor Experience Platform APIs te lezen.

## Volgende stappen {#next-steps}

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het richten aan Reactor API. Selecteer een van de eindpunthulplijnen om aan de slag te gaan:

* [ Reactor API verwijzingsdocumentatie ](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Overzicht van de Reactor-API](/help/tags/api/overview.md)
