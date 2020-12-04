---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Privacys Service
description: Gebruik de RESTful-API om de persoonlijke gegevens van de betrokkenen in Adobe Experience Cloud-toepassingen te beheren
topic: developer guide
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---


# [!DNL Privacy Service] ontwikkelaarsgids

Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u de persoonlijke gegevens van uw betrokkenen (klanten) in Adobe Experience Cloud-toepassingen kunt beheren (openen en verwijderen). [!DNL Privacy Service] voorziet ook een centraal controle en registrerenmechanisme dat u toestaat om tot de status en de resultaten van banen toegang te hebben die [!DNL Experience Cloud] toepassingen impliceren.

In deze handleiding wordt uitgelegd hoe u de [!DNL Privacy Service] API kunt gebruiken. Zie het overzicht [van de gebruikersinterface van de](../ui/overview.md)Privacy Service voor meer informatie over het gebruik van de gebruikersinterface. Zie de [!DNL Privacy Service] API-referentie [voor een uitgebreide lijst met alle beschikbare eindpunten in de](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende [!DNL Experience Platform] functies:

* [[!DNL Privacy Service]](../home.md): Verstrekt een RESTful API en een gebruikersinterface die u toestaan om toegang te beheren en verzoeken van uw gegevenssubjecten (klanten) over Adobe Experience Cloud toepassingen te schrappen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Privacy Service API te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Privacy Service] API te maken, moet u uw toegangsgeloofsbrieven eerst verzamelen die in vereiste kopballen moeten worden gebruikt:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Hiervoor moeten ontwikkelaarsmachtigingen voor [!DNL Experience Platform] de Adobe Admin Console worden verkregen en moeten de gegevens vervolgens worden gegenereerd in de Adobe Developer Console.

### Toegang voor ontwikkelaars verkrijgen tot [!DNL Experience Platform]

Om ontwikkelaarstoegang tot te krijgen [!DNL Platform], volg de eerste stappen in het de authentificatieleerprogramma [van het](../../tutorials/authentication.md)Experience Platform. Zodra u bij de stap &quot;Genereer toegangsgeloofsbrieven in de Console van de Ontwikkelaar van de Adobe&quot;aankomt, terugkeer aan dit leerprogramma om de geloofsbrieven te produceren specifiek voor [!DNL Privacy Service].

### Toegangsreferenties genereren

Gebruikend de Console van de Ontwikkelaar van Adobe, moet u de volgende drie toegangsgeloofsbrieven produceren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Uw `{IMS_ORG}` en `{API_KEY}` hoeven slechts eenmaal te worden gegenereerd en kunnen in toekomstige API-aanroepen opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is echter tijdelijk en moet elke 24 uur opnieuw worden gegenereerd.

De stappen voor het genereren van deze waarden worden hieronder in detail besproken.

#### Eenmalige installatie

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die worden beschreven in de zelfstudie over het [maken van een leeg project](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.

Nadat u een nieuw project hebt gemaakt, klikt u op API **** toevoegen in het scherm **[!UICONTROL Projectoverzicht]** .

![](../images/api/getting-started/add-api-button.png)

Het scherm **[!UICONTROL Een API]** toevoegen wordt weergegeven. Selecteer **[!UICONTROL Privacy Service-API]** in de lijst met beschikbare API&#39;s voordat u op **[!UICONTROL Volgende]** klikt.

![](../images/api/getting-started/add-privacy-service-api.png)

Het scherm **[!UICONTROL Configure API]** verschijnt. Selecteer de optie om een sleutelpaar **[!UICONTROL te]** produceren, dan klik **[!UICONTROL produceer sleutelpaar]** in de bodem-juiste hoek.

![](../images/api/getting-started/generate-key-pair.png)

Het sleutelpaar wordt automatisch geproduceerd, en een dossier van het ZIP dat een privé sleutel en een openbaar certificaat bevat wordt gedownload aan uw lokale machine (die in een recentere stap moet worden gebruikt). Selecteer **[!UICONTROL gevormde API]** opslaan om de configuratie te voltooien.

![](../images/api/getting-started/key-pair-generated.png)

Zodra API aan het project is toegevoegd, verschijnt de projectpagina opnieuw op de **Privacy Service API overzichtspagina** . Van hier, scrol neer aan de sectie van de Rekening van de **[!UICONTROL Dienst (JWT)]** , die de volgende toegangsgeloofsbrieven verstrekt die in alle vraag aan [!DNL Privacy Service] API worden vereist:

* **[!UICONTROL CLIENT-ID]**: De client-id is de vereiste `{API_KEY}` voor die id die moet worden opgegeven in de header x-api-key.
* **[!UICONTROL ORGANISATIE-ID]**: De organisatie-id is de `{IMS_ORG}` waarde die moet worden gebruikt in de header x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Verificatie voor elke sessie

De laatste vereiste referentie die u moet verzamelen, is uw `{ACCESS_TOKEN}`, die wordt gebruikt in de machtigingheader. In tegenstelling tot de waarden voor `{API_KEY}` en `{IMS_ORG}`, moet om de 24 uur een nieuw token worden gegenereerd om API&#39; [!DNL Platform] s te kunnen blijven gebruiken.

Als u een nieuwe sleutel wilt genereren, opent u de eerder gedownloade persoonlijke sleutel en plakt u de inhoud ervan in het tekstvak naast Toegangstoken `{ACCESS_TOKEN}`**[!UICONTROL genereren voordat u op Token]** **** genereren klikt.

![](../images/api/getting-started/paste-private-key.png)

Er wordt een nieuw toegangstoken gegenereerd en er wordt een knop opgegeven waarmee het token naar het klembord kan worden gekopieerd. Deze waarde wordt gebruikt voor de vereiste kopbal van de Vergunning, en moet in het formaat worden verstrekt `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Volgende stappen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het voeren van vraag aan [!DNL Privacy Service] API. Het document over [privacytaken](privacy-jobs.md) doorloopt de verschillende API-aanroepen die u met de [!DNL Privacy Service] API kunt maken. Elke voorbeeldvraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.
