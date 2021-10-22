---
title: Aan de slag met de Privacy Service-API
description: Leer hoe u verificatie uitvoert voor de Privacy Service-API en hoe u voorbeeld-API-aanroepen interpreteert in de documentatie.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 6dcbf2df46ba35104abd9c4e6412799e77c9c49f
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Aan de slag met de Privacy Service-API

Deze gids verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan Privacy Service API te maken.

## Vereisten

Deze handleiding vereist een goed begrip van de volgende functies:

* [Adobe Experience Platform Privacy Service](../home.md): Verstrekt een RESTful API en een gebruikersinterface die u toestaan om toegang te beheren en verzoeken van uw gegevenssubjecten (klanten) over Adobe Experience Cloud toepassingen te schrappen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan Privacy Service API te maken, moet u uw toegangsgeloofsbrieven eerst verzamelen die in vereiste kopballen moeten worden gebruikt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Hiervoor moeten ontwikkelaarsmachtigingen voor Adobe Experience Platform in Adobe Admin Console worden verkregen en moeten de gegevens vervolgens worden gegenereerd in de Adobe Developer Console.

### Toegang tot Experience Platform voor ontwikkelaars

Om ontwikkelaarstoegang te verkrijgen tot [!DNL Platform]volgt u de eerste stappen in het dialoogvenster [Zelfstudie over verificatie van Experience Platforms](https://www.adobe.com/go/platform-api-authentication-en). Zodra u bij de stap &quot;aankomt produceer toegangsgeloofsbrieven in de Console van de Ontwikkelaar van Adobe&quot;, terugkeer aan dit leerprogramma om de geloofsbrieven te produceren specifiek voor Privacy Service.

### Toegangsreferenties genereren

Gebruikend de Console van de Ontwikkelaar van Adobe, moet u de volgende drie toegangsgeloofsbrieven produceren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Uw `{IMS_ORG}` en `{API_KEY}` moet slechts eenmaal worden gegenereerd en kan in toekomstige API-aanroepen opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is tijdelijk en moet om de 24 uur opnieuw worden gegenereerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

#### Eenmalige installatie

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die in de zelfstudie worden beschreven [een leeg project maken](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.

Als u een nieuw project hebt gemaakt, selecteert u **[!UICONTROL Add API]** op de **[!UICONTROL Project Overview]** scherm.

![](../images/api/getting-started/add-api-button.png)

De **[!UICONTROL Add an API]** wordt weergegeven. Selecteren **[!UICONTROL Privacy Service API]** uit de lijst met beschikbare API&#39;s voordat u **[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

De **[!UICONTROL Configure API]** wordt weergegeven. Selecteer de optie die u wilt **[!UICONTROL Generate a key pair]** selecteert u vervolgens **[!UICONTROL Generate keypair]** in de rechterbenedenhoek.

![](../images/api/getting-started/generate-key-pair.png)

Het sleutelpaar wordt automatisch geproduceerd, en een dossier van het ZIP dat een privé sleutel en een openbaar certificaat bevat wordt gedownload aan uw lokale machine (die in een recentere stap moet worden gebruikt). Selecteren **[!UICONTROL Save configured API]** om de configuratie te voltooien.

![](../images/api/getting-started/key-pair-generated.png)

Zodra API aan het project is toegevoegd, verschijnt de projectpagina opnieuw op het **Overzicht van Privacy Service-API** pagina. Hier omlaag schuiven naar de **[!UICONTROL Service Account (JWT)]** sectie, die de volgende toegangsgeloofsbrieven verstrekt die in alle vraag aan Privacy Service API worden vereist:

* **[!UICONTROL CLIENT ID]**: De client-id is vereist `{API_KEY}` hiervoor moet in de x-api-key header worden voorzien.
* **[!UICONTROL ORGANIZATION ID]**: De organisatie-id is de `{IMS_ORG}` waarde die moet worden gebruikt in de x-gw-ims-org-id header.

![](../images/api/getting-started/jwt-credentials.png)

#### Verificatie voor elke sessie

De laatste vereiste referentie die u moet verzamelen is uw `{ACCESS_TOKEN}`, die wordt gebruikt in de kop Autorisatie. In tegenstelling tot de waarden voor `{API_KEY}` en `{IMS_ORG}`moet om de 24 uur een nieuw token worden gegenereerd om verder te kunnen gaan met [!DNL Platform] API&#39;s.

Een nieuwe `{ACCESS_TOKEN}`, opent u de eerder gedownloade persoonlijke sleutel en plakt u de inhoud ervan in het tekstvak naast **[!UICONTROL Generate access token]** voordat u selecteert **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste koptekst voor autorisatie en moet worden opgegeven in de notatie `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/api-guide.md#sample-api) in de gids Aan de slag voor Platform APIs.

## Volgende stappen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het maken vraag aan Privacy Service API. Selecteer een van de eindpunthulplijnen om aan de slag te gaan:

* [Privacytaken](./privacy-jobs.md)
* [Toestemming](./consent.md)
