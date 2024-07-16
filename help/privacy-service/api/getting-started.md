---
title: De Privacy Service-API verifiëren en openen
description: Leer hoe u verificatie uitvoert voor de Privacy Service-API en hoe u voorbeeld-API-aanroepen interpreteert in de documentatie.
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---

# De Privacy Service-API verifiëren en openen

Deze gids verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan Adobe Experience Platform Privacy Service API te maken.

## Vereisten {#prerequisites}

Deze gids vereist een werkend begrip van [ Privacy Service ](../home.md) en hoe het u toestaat om toegang te beheren en verzoeken van uw gegevensproefpersonen (klanten) over de toepassingen van Adobe Experience Cloud te schrappen.

Als u toegangsreferenties voor de API wilt maken, moet een beheerder binnen uw organisatie eerder productprofielen hebben ingesteld voor Privacy Service binnen Adobe Admin Console. Het productprofiel dat u toewijst aan een API-integratie, bepaalt welke machtigingen integratie heeft wanneer u toegang krijgt tot Privacy Service-mogelijkheden. Zie de gids over [ het beheren van de toestemmingen van de Privacy Service ](../permissions.md) voor meer informatie.

## Waarden verzamelen voor vereiste koppen {#gather-values-required-headers}

Om vraag aan Privacy Service API te maken, moet u uw toegangsgeloofsbrieven eerst verzamelen die in vereiste kopballen moeten worden gebruikt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Deze waarden worden geproduceerd gebruikend [ Adobe Developer Console ](https://developer.adobe.com/console). Uw `{ORG_ID}` en `{API_KEY}` hoeven slechts eenmaal te worden gegenereerd en kunnen in toekomstige API-aanroepen opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is echter tijdelijk en moet elke 24 uur opnieuw worden gegenereerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

### Eenmalige installatie {#one-time-setup}

Ga naar [ Adobe Developer Console ](https://developer.adobe.com/console) en teken binnen met uw Adobe ID. Daarna, volg de stappen die in het leerprogramma worden geschetst op [ creërend een leeg project ](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in de documentatie van Developer Console.

Als u een nieuw project hebt gemaakt, selecteert u **[!UICONTROL Add to Project]** en kiest u **[!UICONTROL API]** in het vervolgkeuzemenu.

![ de API optie die van [!UICONTROL Add to Project] dropdown van de pagina van projectdetails in Developer Console wordt geselecteerd ](../images/api/getting-started/add-api-button.png)

#### Selecteer de Privacy Service-API {#select-privacy-service-api}

Het scherm **[!UICONTROL Add an API]** wordt weergegeven. Selecteer **[!UICONTROL Experience Cloud]** om de lijst met beschikbare API&#39;s te beperken en selecteer vervolgens de kaart voor **[!UICONTROL Privacy Service API]** voordat u **[!UICONTROL Next]** selecteert.

![ de Privacy Service API kaart die van de lijst van beschikbare APIs wordt geselecteerd ](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>Selecteer de **[!UICONTROL View docs]** optie om in een afzonderlijk browser venster aan de volledige [ Privacy Service API verwijzingsdocumentatie ](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) te navigeren.

Selecteer vervolgens het verificatietype dat u wilt maken voor het genereren van toegangstokens en voor toegang tot de Privacy Service-API.

>[!IMPORTANT]
>
>Selecteer de methode **[!UICONTROL OAuth Server-to-Server]** omdat dit de enige methode is die u kunt gebruiken om door te gaan. De methode **[!UICONTROL Service Account (JWT)]** is vervangen. Terwijl de integratie die de authentificatiemethode JWT gebruikt tot 1 Januari, 2025 zal blijven werken, adviseert de Adobe sterk dat u bestaande integratie aan de nieuwe server-aan-server methode OAuth vóór die datum migreert. Krijg meer informatie in de sectie [!BADGE  Afgekeurd ]{type=negative}[ produceer een Token van het Web JSON (JWT) ](/help/landing/api-authentication.md#jwt).

![ Uitgezochte Oauth server-aan-Server authentificatiemethode.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### Machtigingen toewijzen via productprofielen {#product-profiles}

De laatste configuratiestap bestaat uit het selecteren van de productprofielen waarvan deze integratie de machtigingen erft. Als u meer dan één profiel selecteert, worden de rechtensets gecombineerd voor de integratie.

>[!NOTE]
>
Productprofielen en de bijbehorende granulaire machtigingen worden door beheerders gemaakt en beheerd via Adobe Admin Console. Zie de gids op [ toestemmingen van de Privacy Service ](../permissions.md) voor meer informatie.

Selecteer **[!UICONTROL Save configured API]** als u klaar bent.

![ één enkel productprofiel dat van de lijst wordt geselecteerd alvorens de configuratie ](../images/api/getting-started/select-product-profiles.png) op te slaan

Zodra API aan het project is toegevoegd, **[!UICONTROL Privacy Service API]** toont de pagina voor het project de volgende geloofsbrieven die in alle vraag aan Privacy Service APIs worden vereist:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![ de informatie van de Integratie na het toevoegen van API in Developer Console.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### Verificatie voor elke sessie {#authentication-each-session}

De laatste vereiste referentie die u moet verzamelen, is de `{ACCESS_TOKEN}` , die wordt gebruikt in de machtigingheader. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}` , moet om de 24 uur een nieuw token worden gegenereerd om de API te kunnen blijven gebruiken.

Over het algemeen zijn er twee methoden om een toegangstoken te genereren:

* [ produceer manueel het teken ](#manual-token) voor het testen en ontwikkeling.
* [ Automatiseer symbolische generatie ](#auto-token) voor API integratie.

#### Een token handmatig genereren {#manual-token}

Als u handmatig een nieuwe `{ACCESS_TOKEN}` wilt genereren, navigeert u naar **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** en selecteert u **[!UICONTROL Generate access token]** (zie hieronder).

![ het schermopname van A van hoe een toegangstoken in Developer Console UI wordt geproduceerd.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste [!DNL Authorization] header en moet worden opgegeven in de indeling `Bearer {ACCESS_TOKEN}` .

#### Automatisch token genereren {#auto-token}

U kunt ook een Postman-omgeving en -verzameling gebruiken om toegangstokens te genereren. Voor meer informatie, lees de sectie over [ gebruikend Postman om API vraag ](/help/landing/api-authentication.md#use-postman) in de Experience Platform API authentificatiegids voor authentiek te verklaren en te testen.

## API-voorbeeldaanroepen lezen {#read-sample-api-calls}

Elke eindpuntgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te voorbeeld API vraag ](../../landing/api-guide.md#sample-api) in de begonnen gids voor Platform APIs lezen.

## Volgende stappen {#next-steps}

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het maken vraag aan Privacy Service API. Selecteer een van de eindpunthulplijnen om aan de slag te gaan:

* [Privacytaken](./privacy-jobs.md)
* [Toestemming](./consent.md)
