---
keywords: Experience Platform;home;populaire onderwerpen;exporteren;Exporteren
solution: Experience Platform
title: Gebruikershandleiding voor Privacy Service
topic: UI guide
description: Leer hoe u de gebruikersinterface van de Privacy Service gebruikt om privacyverzoeken in verschillende Experience Cloud-toepassingen te coördineren en te controleren.
translation-type: tm+mt
source-git-commit: 238a9200e4b43d41335bed0efab079780b252717
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---


# [!DNL Privacy Service] gebruikershandleiding

Dit document bevat stappen voor het maken en beheren van privacyverzoeken met behulp van de [!DNL Privacy Service]-gebruikersinterface.

## Door het UI-dashboard [!DNL Privacy Service] bladeren

Het dashboard voor [!DNL Privacy Service] UI verstrekt twee widgets die u toestaan om de status van uw privacybanen te bekijken: &quot;[!UICONTROL Statusrapport]&quot; en &quot;[!UICONTROL Taakverzoeken]&quot;. Op het dashboard wordt ook de huidige geselecteerde regelgeving voor de weergegeven taken weergegeven.

![UI-dashboard](../images/user-guide/dashboard.png)

### Type verordening

[!DNL Privacy Service] ondersteunt aanvragen voor een baan voor verschillende privacyregels:

* De [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* De [!DNL General Data Protection Regulation] van de Europese Unie ([!UICONTROL GDPR])
* Thailand [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Brazilië [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Nieuw-Zeeland [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Taken voor elk type regelgeving worden afzonderlijk bijgehouden. Als u wilt schakelen tussen regelgevingstypen, selecteert u het vervolgkeuzemenu **[!UICONTROL Type voorschrift]** en selecteert u de gewenste verordening in de lijst.

![Vervolgkeuzelijst Type](../images/user-guide/regulation.png)

Als u het regulatietype wijzigt, wordt het dashboard bijgewerkt en worden alle bewerkingen, filters, widgets en dialoogvensters voor het creëren van werkgelegenheid weergegeven die van toepassing zijn op de geselecteerde verordening.

![Bijgewerkt dashboard](../images/user-guide/dashboard-update.png)

### Statusrapport

De grafiek aan de linkerkant van de widgetsporen van het Rapport van de Status legde banen tegen om het even welke banen voor die met fouten zouden kunnen zijn gemeld. In de grafiek aan de rechterkant worden taken bijgehouden aan het einde van het nalevingsvenster van 30 dagen.

Selecteer een van de twee schakelknoppen boven de grafiek om de desbetreffende cijfers weer te geven of te verbergen.

![](../images/user-guide/hide-errors.png)

U kunt het exacte aantal taken dat aan elk gegevenspunt op de grafieken is gekoppeld, weergeven door de muis boven het desbetreffende gegevenspunt te plaatsen.

![Gegevenspunten bij aanwijzen met muis](../images/user-guide/mouse-over.png)

Als u meer details over een bepaald gegevenspunt wilt weergeven, selecteert u het desbetreffende gegevenspunt om de bijbehorende taken weer te geven in de widget Taakverzoeken. Neem nota van het filter dat net boven de baanlijst wordt toegepast.

![Toegepast filter van widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Wanneer een filter op de widget Taakverzoeken is toegepast, kunt u het filter verwijderen door de **X** op de filtervulling te selecteren. De Verzoeken van de baan keren dan aan het gebrek volgende lijst terug.

### Taakverzoeken

De widget Taakverzoeken bevat een lijst met alle beschikbare taakaanvragen in uw organisatie, inclusief gegevens zoals het type aanvraag, de huidige status, de vervaldatum en het e-mailadres van de aanvrager.

>[!NOTE]
>
>De gegevens voor eerder gecreëerde banen zijn slechts 30 dagen na de voltooiingsdatum toegankelijk.

U kunt de lijst filteren door trefwoorden in de zoekbalk onder de titel Taakverzoeken te typen. De lijst filtert automatisch terwijl u typt, tonend verzoeken die waarden bevatten die uw onderzoekstermijnen aanpassen. U kunt ook het vervolgkeuzemenu **[!UICONTROL Gevraagd op]** gebruiken om een tijdbereik voor de weergegeven taken te selecteren.

![Zoekopties voor taakaanvraag](../images/user-guide/job-search.png)

Als u de details van een bepaalde taakaanvraag wilt weergeven, selecteert u de taak-id van de aanvraag in de lijst om de pagina **[!UICONTROL Taakdetails]** te openen.

![Taakgegevens GDPR-gebruikersinterface](../images/user-guide/job-details.png)

Dit dialoogvenster bevat statusinformatie over elke [!DNL Experience Cloud]-oplossing en de huidige status ten opzichte van de algemene taak. Aangezien elke privacybaan asynchroon is, toont de pagina de recentste communicatie datum en tijd (GMT) van elke oplossing, aangezien sommige meer tijd dan anderen vereisen om het verzoek te verwerken.

Als een oplossing om het even welke extra gegevens heeft verstrekt, is het viewable in deze dialoog. U kunt deze gegevens weergeven door afzonderlijke productrijen te selecteren.

Als u de volledige taakgegevens als CSV-bestand wilt downloaden, selecteert u **[!UICONTROL Exporteren naar CSV]** rechtsboven in het dialoogvenster.

## Een nieuw verzoek voor een privacytaak maken

>[!NOTE]
>
>Als u een privacytaakverzoek wilt maken, moet u identiteitsgegevens opgeven voor de specifieke klanten van wie de gegevens moeten worden benaderd of verwijderd. Controleer het document op [identiteitsgegevens voor privacyverzoeken](../identity-data.md) voordat u doorgaat met deze sectie.

De interface [!DNL Privacy Service] biedt twee methoden om nieuwe taakaanvragen te maken:

* [De Request Builder gebruiken](#request-builder)
* [Een JSON-bestand uploaden](#json)

De stappen voor het gebruiken van elk van deze methodes worden verstrekt in de volgende secties.

### De Request Builder {#request-builder} gebruiken

Met de Request Builder kunt u handmatig een nieuw verzoek voor een privacytaak maken in de gebruikersinterface. De Bouwer van het Verzoek wordt best gebruikt voor eenvoudigere en kleinere reeksen verzoeken, omdat de de grensverzoeken van de Bouwer van het Verzoek om slechts identiteitskaart type per gebruiker te hebben. Voor complexere verzoeken, kan het beter zijn om [een JSON dossier](#json) in plaats daarvan te uploaden.

Om te beginnen gebruikend de Bouwer van het Verzoek, uitgezocht **[!UICONTROL Create Verzoek]** onder de widget van het Rapport van de Status op de rechterkant van het scherm.

![Aanvraag maken selecteren](../images/user-guide/create-request.png)

Het dialoogvenster **[!UICONTROL Aanvraag maken]** wordt geopend en hierin worden de beschikbare opties weergegeven voor het indienen van een aanvraag voor een privacytaak voor het momenteel geselecteerde regulatietype.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Selecteer **[!UICONTROL Taaktype]** van het verzoek (&quot;Schrapping&quot;of &quot;Toegang&quot;) en één of meerdere beschikbare producten van de lijst.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Selecteer onder **[!UICONTROL Namespace type]** het juiste naamruimtetype voor de klant-id&#39;s die naar [!DNL Privacy Service] worden verzonden.

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Wanneer het gebruiken van het standaardnamespacetype, selecteer een namespace van het drop-down menu (e-mail, ECID, of STEUN), dan typ de waarden van identiteitskaart in textbox aan het recht, drukkend **\&lt;enter>** voor elke identiteitskaart om het aan de lijst toe te voegen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Wanneer u het aangepaste naamruimtetype gebruikt, moet u de naamruimte handmatig typen voordat u de onderstaande id-waarden opgeeft.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Selecteer **[!UICONTROL Maken]** als u klaar bent.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Het dialoogvenster verdwijnt en de nieuwe taak (of taken) worden samen met de huidige verwerkingsstatus weergegeven in de widget Taakverzoeken.

### Een JSON-bestand {#json} uploaden

Wanneer u complexere aanvragen maakt, zoals aanvragen die meerdere id-typen gebruiken voor elke gegevenssubject die wordt verwerkt, kunt u een aanvraag maken door een JSON-bestand te uploaden.

Selecteer de pijl naast **[!UICONTROL Verzoek maken]**, onder de widget Statusrapport aan de rechterkant van het scherm. Selecteer **[!UICONTROL JSON]** uploaden in de lijst met opties die wordt weergegeven.

![Aanmaakopties aanvragen](../images/user-guide/create-options.png)

Het dialoogvenster **[!UICONTROL JSON uploaden]** wordt weergegeven en bevat een venster waarin u uw JSON-bestand kunt slepen en neerzetten.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Als u geen JSON-bestand hebt om te uploaden, selecteert u **[!UICONTROL Adobe-GDPR-Request.json]** downloaden om een sjabloon te downloaden dat u kunt vullen op basis van de waarden die u van de betrokkenen hebt verzameld.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Zoek het JSON-bestand op uw computer en sleep het naar het dialoogvenster. Als het uploaden is voltooid, wordt de bestandsnaam weergegeven in het dialoogvenster. U kunt desgewenst meer JSON-bestanden toevoegen door deze naar het dialoogvenster te slepen.

Selecteer **[!UICONTROL Maken]** als u klaar bent. Het dialoogvenster verdwijnt en de nieuwe taak (of taken) worden samen met de huidige verwerkingsstatus weergegeven in de widget Taakverzoeken.

### Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u de interface [!DNL Privacy Service] kunt gebruiken om een privacytaak te maken, de details van een taak te bekijken en de verwerkingsstatus ervan te controleren en de resultaten te downloaden zodra deze zijn voltooid.

Raadpleeg de [handleiding voor ontwikkelaars](../api/getting-started.md) voor informatie over het programmatisch uitvoeren van deze bewerkingen met de [!DNL Privacy Service]-API.