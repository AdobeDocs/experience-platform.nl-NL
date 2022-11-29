---
title: Aan de slag met de Privacy Service-API
description: Leer hoe u verificatie uitvoert voor de Privacy Service-API en hoe u voorbeeld-API-aanroepen interpreteert in de documentatie.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# Aan de slag met de Privacy Service-API

Deze gids verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan Adobe Experience Platform Privacy Service API te maken.

## Vereisten

Deze handleiding vereist een goed begrip van [Privacy Service](../home.md) en hoe u hiermee toegang kunt beheren en aanvragen van uw betrokkenen (klanten) kunt verwijderen voor alle Adobe Experience Cloud-toepassingen.

Als u toegangsreferenties voor de API wilt maken, moet een beheerder binnen uw organisatie eerder productprofielen hebben ingesteld voor Privacy Service binnen Adobe Admin Console. Het productprofiel dat u toewijst aan een API-integratie, bepaalt welke machtigingen integratie heeft wanneer u toegang krijgt tot Privacy Service-mogelijkheden. Zie de handleiding op [beheren, machtigingen voor Privacy Service](../permissions.md) voor meer informatie .

## Waarden verzamelen voor vereiste koppen

Om vraag aan Privacy Service API te maken, moet u uw toegangsgeloofsbrieven eerst verzamelen die in vereiste kopballen moeten worden gebruikt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Deze waarden worden gegenereerd met [Adobe Developer Console](https://developer.adobe.com/console). Uw `{ORG_ID}` en `{API_KEY}` moet slechts eenmaal worden gegenereerd en kan in toekomstige API-aanroepen opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is tijdelijk en moet om de 24 uur opnieuw worden gegenereerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

### Eenmalige installatie

Ga naar [Adobe Developer Console](https://developer.adobe.com/console) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die in de zelfstudie worden beschreven [een leeg project maken](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in de documentatie van de Developer Console.

Als u een nieuw project hebt gemaakt, selecteert u **[!UICONTROL Add to Project]** en kiest u **[!UICONTROL API]** in het vervolgkeuzemenu.

![De API-optie die wordt geselecteerd in het menu [!UICONTROL Add to Project] vervolgkeuzelijst van de pagina met projectdetails in Developer Console](../images/api/getting-started/add-api-button.png)

#### Een API selecteren en een sleutelpaar genereren {#keypair}

De **[!UICONTROL Add an API]** wordt weergegeven. Selecteren **[!UICONTROL Experience Cloud]** om de lijst met beschikbare API&#39;s te beperken, selecteert u vervolgens de kaart voor **[!UICONTROL Privacy Service API]** voordat u selecteert **[!UICONTROL Next]**.

![De Privacy Service-API-kaart die wordt geselecteerd in de lijst met beschikbare API&#39;s](../images/api/getting-started/add-privacy-service-api.png)

De **[!UICONTROL Configure API]** wordt weergegeven. Selecteer de optie die u wilt **[!UICONTROL Generate a key pair]** selecteert u vervolgens **[!UICONTROL Generate keypair]**.

![De [!UICONTROL Generate a key pair] optie die op [!UICONTROL Configure API] scherm](../images/api/getting-started/generate-key-pair.png)

Het sleutelpaar wordt automatisch geproduceerd en een dossier van het PIT dat een privé sleutel en een openbaar certificaat bevat wordt gedownload door uw browser (die in een recentere stap moet worden gebruikt). Selecteren **[!UICONTROL Next]** om door te gaan.

![Het gegenereerde sleutelpaar dat in de gebruikersinterface wordt weergegeven, waarvan de waarden automatisch door de browser worden gedownload](../images/api/getting-started/key-pair-generated.png)

#### Machtigingen toewijzen via productprofielen {#product-profiles}

De laatste configuratiestap bestaat uit het selecteren van de productprofielen waarvan deze integratie de machtigingen erft. Als u meer dan één profiel selecteert, worden de rechtensets gecombineerd voor de integratie.

>[!NOTE]
>
>Productprofielen en de bijbehorende granulaire machtigingen worden door beheerders gemaakt en beheerd via Adobe Admin Console. Zie de handleiding op [Machtigingen voor Privacy Service](../permissions.md) voor meer informatie .

Als u klaar bent, selecteert u **[!UICONTROL Save configured API]**.

![Eén enkel productprofiel dat wordt geselecteerd in de lijst voordat de configuratie wordt opgeslagen](../images/api/getting-started/select-product-profiles.png)

Zodra API aan het project is toegevoegd, verschijnt de projectpagina opnieuw op het **Overzicht van Privacy Service-API** pagina. Hier omlaag schuiven naar de **[!UICONTROL Service Account (JWT)]** sectie, die de volgende toegangsgeloofsbrieven verstrekt die in alle vraag aan Privacy Service API worden vereist:

* **[!UICONTROL CLIENT ID]**: De client-id is vereist `{API_KEY}` die in de `x-api-key` header.
* **[!UICONTROL ORGANIZATION ID]**: De organisatie-id is de `{ORG_ID}` waarde die moet worden gebruikt in de `x-gw-ims-org-id` header.

![De waarden van de identiteitskaart van de Cliënt en van identiteitskaart van de Organisatie zoals zij op de pagina van het projectoverzicht verschijnen nadat API is gevormd](../images/api/getting-started/jwt-credentials.png)

### Verificatie voor elke sessie

De laatste vereiste referentie die u moet verzamelen is uw `{ACCESS_TOKEN}`, die wordt gebruikt in de kop Autorisatie. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}`moet om de 24 uur een nieuw token worden gegenereerd om de API te kunnen blijven gebruiken.

Over het algemeen zijn er twee methoden om een toegangstoken te genereren:

* [De token handmatig genereren](#manual-token) voor tests en ontwikkeling.
* [Automatisch token genereren](#auto-token) voor API-integratie.

#### Een token handmatig genereren {#manual-token}

Om een nieuwe manueel te produceren `{ACCESS_TOKEN}`, opent u de eerder gedownloade persoonlijke sleutel en plakt u de inhoud ervan in het tekstvak naast **[!UICONTROL Generate access token]** voordat u selecteert **[!UICONTROL Generate Token]**.

![Het eerder gegenereerde toegangstoken dat op de overzichtspagina van het project wordt geplakt, met de [!UICONTROL Generate Token] knop die wordt geselecteerd na](../images/api/getting-started/paste-private-key.png)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste koptekst voor autorisatie en moet worden opgegeven in de notatie `Bearer {ACCESS_TOKEN}`.

![Het gegenereerde toegangstoken dat wordt gekopieerd van de UI](../images/api/getting-started/generated-access-token.png)

#### Automatisch token genereren {#auto-token}

U kunt nieuwe toegangstokens voor geautomatiseerde processen produceren door een Token van het Web JSON (JWT) door een verzoek van de POST naar de Dienst van Adobe Identity Management (IMS) te verzenden. Zie het document Developer Console op [JWT-verificatie](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) voor gedetailleerde stappen.

## API-voorbeeldaanroepen lezen

Elke eindpuntgids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/api-guide.md#sample-api) in de gids Aan de slag voor Platform APIs.

## Volgende stappen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het maken vraag aan Privacy Service API. Selecteer een van de eindpunthulplijnen om aan de slag te gaan:

* [Privacytaken](./privacy-jobs.md)
* [Toestemming](./consent.md)
