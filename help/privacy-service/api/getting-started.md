---
title: De Privacy Service-API verifiëren en openen
description: Leer hoe u verificatie uitvoert voor de Privacy Service-API en hoe u voorbeeld-API-aanroepen interpreteert in de documentatie.
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# De Privacy Service-API verifiëren en openen

Deze gids verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan Adobe Experience Platform Privacy Service API te maken.

## Vereisten {#prerequisites}

Deze handleiding vereist een goed begrip van [Privacy Service](../home.md) en hoe u hiermee toegang kunt beheren en aanvragen van uw betrokkenen (klanten) kunt verwijderen voor alle Adobe Experience Cloud-toepassingen.

Als u toegangsreferenties voor de API wilt maken, moet een beheerder binnen uw organisatie eerder productprofielen hebben ingesteld voor Privacy Service binnen Adobe Admin Console. Het productprofiel dat u toewijst aan een API-integratie, bepaalt welke machtigingen integratie heeft wanneer u toegang krijgt tot Privacy Service-mogelijkheden. Zie de handleiding op [beheren, machtigingen voor Privacy Service](../permissions.md) voor meer informatie .

## Waarden verzamelen voor vereiste koppen {#gather-values-required-headers}

Om vraag aan Privacy Service API te maken, moet u uw toegangsgeloofsbrieven eerst verzamelen die in vereiste kopballen moeten worden gebruikt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Deze waarden worden gegenereerd met [Adobe Developer Console](https://developer.adobe.com/console). Uw `{ORG_ID}` en `{API_KEY}` moet slechts eenmaal worden gegenereerd en kan in toekomstige API-aanroepen opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is tijdelijk en moet om de 24 uur opnieuw worden gegenereerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

### Eenmalige installatie {#one-time-setup}

Ga naar [Adobe Developer Console](https://developer.adobe.com/console) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die in de zelfstudie worden beschreven [een leeg project maken](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in de documentatie van de Developer Console.

Als u een nieuw project hebt gemaakt, selecteert u **[!UICONTROL Add to Project]** en kiest u **[!UICONTROL API]** in het vervolgkeuzemenu.

![De API-optie die wordt geselecteerd in het menu [!UICONTROL Add to Project] vervolgkeuzelijst van de pagina met projectdetails in Developer Console](../images/api/getting-started/add-api-button.png)

#### Selecteer de Privacy Service-API {#select-privacy-service-api}

De **[!UICONTROL Add an API]** wordt weergegeven. Selecteren **[!UICONTROL Experience Cloud]** om de lijst met beschikbare API&#39;s te beperken, selecteert u vervolgens de kaart voor **[!UICONTROL Privacy Service API]** voordat u selecteert **[!UICONTROL Next]**.

![De Privacy Service-API-kaart die wordt geselecteerd in de lijst met beschikbare API&#39;s](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>Selecteer de **[!UICONTROL View docs]** om in een afzonderlijk browservenster naar het volledige venster te navigeren [Privacy Service API-naslagdocumentatie](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

Selecteer vervolgens het verificatietype dat u wilt maken voor het genereren van toegangstokens en voor toegang tot de Privacy Service-API.

>[!IMPORTANT]
>
>Selecteer de **[!UICONTROL OAuth Server-to-Server]** -methode, aangezien dit de enige methode is die wordt ondersteund om verder te gaan. De **[!UICONTROL Service Account (JWT)]** is vervangen. Terwijl de integratie die de authentificatiemethode JWT gebruikt tot 1 Januari, 2025 zal blijven werken, adviseert de Adobe sterk dat u bestaande integratie aan de nieuwe server-aan-server methode OAuth vóór die datum migreert. Meer informatie ophalen in de sectie [!BADGE Vervangen]{type=negative}[Een JSON-webtoken (JWT) genereren](/help/landing/api-authentication.md#jwt).

![Selecteer Oauth Server-aan-Server authentificatiemethode.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### Machtigingen toewijzen via productprofielen {#product-profiles}

De laatste configuratiestap bestaat uit het selecteren van de productprofielen waarvan deze integratie de machtigingen erft. Als u meer dan één profiel selecteert, worden de rechtensets gecombineerd voor de integratie.

>[!NOTE]
>
Productprofielen en de bijbehorende granulaire machtigingen worden door beheerders gemaakt en beheerd via Adobe Admin Console. Zie de handleiding op [Machtigingen voor Privacy Service](../permissions.md) voor meer informatie .

Selecteer **[!UICONTROL Save configured API]**.

![Eén enkel productprofiel dat wordt geselecteerd in de lijst voordat de configuratie wordt opgeslagen](../images/api/getting-started/select-product-profiles.png)

Zodra API aan het project is toegevoegd, **[!UICONTROL Privacy Service API]** De pagina voor het project toont de volgende geloofsbrieven die in alle vraag aan Privacy Service APIs worden vereist:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![Integratiegegevens na het toevoegen van een API in de Developer Console.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### Verificatie voor elke sessie {#authentication-each-session}

De laatste vereiste referentie die u moet verzamelen is uw `{ACCESS_TOKEN}`, die wordt gebruikt in de kop Autorisatie. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}`moet om de 24 uur een nieuw token worden gegenereerd om de API te kunnen blijven gebruiken.

Over het algemeen zijn er twee methoden om een toegangstoken te genereren:

* [De token handmatig genereren](#manual-token) voor tests en ontwikkeling.
* [Automatisch token genereren](#auto-token) voor API-integratie.

#### Een token handmatig genereren {#manual-token}

Om een nieuwe manueel te produceren `{ACCESS_TOKEN}`, navigeer naar **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** en selecteert u **[!UICONTROL Generate access token]**, zoals hieronder weergegeven.

![Een het schermopname van hoe een toegangstoken in de UI van de Console van de Ontwikkelaar wordt geproduceerd.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste [!DNL Authorization] en moet worden opgegeven in de vorm `Bearer {ACCESS_TOKEN}`.

#### Automatisch token genereren {#auto-token}

U kunt ook een Postman-omgeving en -verzameling gebruiken om toegangstokens te genereren. Lees voor meer informatie de sectie over [het gebruiken van Postman om API vraag voor authentiek te verklaren en te testen](/help/landing/api-authentication.md#use-postman) in de Experience Platform API-verificatiegids.

## API-voorbeeldaanroepen lezen {#read-sample-api-calls}

Elke eindpuntgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/api-guide.md#sample-api) in de gids Aan de slag voor Platform APIs.

## Volgende stappen {#next-steps}

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het maken vraag aan Privacy Service API. Selecteer een van de eindpunthulplijnen om aan de slag te gaan:

* [Privacytaken](./privacy-jobs.md)
* [Toestemming](./consent.md)
