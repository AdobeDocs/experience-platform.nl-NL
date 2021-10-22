---
keywords: Experience Platform;home;populaire onderwerpen;exporteren;Exporteren
solution: Experience Platform
title: Privacy-taken beheren in de gebruikersinterface van de Privacy Service
topic-legacy: UI guide
description: Leer hoe u de gebruikersinterface van de Privacy Service gebruikt om privacyverzoeken in verschillende Experience Cloud-toepassingen te coördineren en te controleren.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---

# Privacy-taken beheren in de gebruikersinterface van de Privacy Service

Dit document bevat stappen voor het maken en beheren van privacyverzoeken met de [!DNL Privacy Service] gebruikersinterface.

## Bladeren in het dialoogvenster [!DNL Privacy Service] UI-dashboard

Het dashboard voor de [!DNL Privacy Service] De gebruikersinterface bevat twee widgets waarmee u de status van uw privacytaken kunt weergeven: &quot;[!UICONTROL Status Report]&quot; en &quot;[!UICONTROL Job Requests]&quot;. Op het dashboard wordt ook de huidige geselecteerde regelgeving voor de weergegeven taken weergegeven.

![UI-dashboard](../images/user-guide/dashboard.png)

### Type verordening

[!DNL Privacy Service] ondersteunt aanvragen voor een baan voor verschillende privacyregels:

* De [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* De [!DNL General Data Protection Regulation] ([!UICONTROL GDPR])
* Thailand [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Brazilië [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* Nieuw-Zeeland [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Taken voor elk type regelgeving worden afzonderlijk bijgehouden. Als u wilt schakelen tussen regelgevingstypen, selecteert u de optie **[!UICONTROL Regulation Type]** en selecteer de gewenste verordening in de lijst.

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
>Wanneer een filter is toegepast op de widget Taakverzoeken, kunt u het filter verwijderen door het **X** op de filterpil. De Verzoeken van de baan keren dan aan het gebrek volgende lijst terug.

### Taakverzoeken

De widget Taakverzoeken bevat een lijst met alle beschikbare taakaanvragen in uw organisatie, inclusief gegevens zoals het type aanvraag, de huidige status, de vervaldatum en het e-mailadres van de aanvrager.

>[!NOTE]
>
>De gegevens voor eerder gecreëerde banen zijn slechts 30 dagen na de voltooiingsdatum toegankelijk.

U kunt de lijst filteren door trefwoorden in de zoekbalk onder de titel Taakverzoeken te typen. De lijst filtert automatisch terwijl u typt, tonend verzoeken die waarden bevatten die uw onderzoekstermijnen aanpassen. U kunt ook de opdracht **[!UICONTROL Requested on]** vervolgkeuzelijst om een tijdbereik te selecteren voor de weergegeven taken.

![Zoekopties voor taakaanvraag](../images/user-guide/job-search.png)

Als u de details van een bepaalde taakaanvraag wilt bekijken, selecteert u de taak-id van de aanvraag in de lijst om de opdracht **[!UICONTROL Job Details]** pagina.

![Taakgegevens GDPR-gebruikersinterface](../images/user-guide/job-details.png)

Dit dialoogvenster bevat statusinformatie over elk [!DNL Experience Cloud] oplossing en de huidige toestand in verhouding tot de algemene taak. Aangezien elke privacybaan asynchroon is, toont de pagina de recentste communicatie datum en tijd (GMT) van elke oplossing, aangezien sommige meer tijd dan anderen vereisen om het verzoek te verwerken.

Als een oplossing om het even welke extra gegevens heeft verstrekt, is het viewable in deze dialoog. U kunt deze gegevens weergeven door afzonderlijke productrijen te selecteren.

Selecteer **[!UICONTROL Export to CSV]** rechtsboven in het dialoogvenster.

## Een nieuw verzoek voor een privacytaak maken

>[!NOTE]
>
>Als u een privacytaakverzoek wilt maken, moet u identiteitsgegevens opgeven voor de specifieke klanten van wie de gegevens moeten worden benaderd of verwijderd. Controleer het document op [identiteitsgegevens voor privacyverzoeken](../identity-data.md) voordat u doorgaat met deze sectie.

De [!DNL Privacy Service] UI biedt twee methoden om nieuwe taakaanvragen te maken:

* [De Request Builder gebruiken](#request-builder)
* [Een JSON-bestand uploaden](#json)

De stappen voor het gebruiken van elk van deze methodes worden verstrekt in de volgende secties.

### De Request Builder gebruiken {#request-builder}

Met de Request Builder kunt u handmatig een nieuw verzoek voor een privacytaak maken in de gebruikersinterface. De Bouwer van het Verzoek wordt best gebruikt voor eenvoudigere en kleinere reeksen verzoeken, omdat de de grensverzoeken van de Bouwer van het Verzoek om slechts identiteitskaart type per gebruiker te hebben. Voor meer gecompliceerde verzoeken kan het beter zijn om [een JSON-bestand uploaden](#json) in plaats daarvan.

Selecteer **[!UICONTROL Create Request]** onder de widget Statusrapport aan de rechterkant van het scherm.

![Aanvraag maken selecteren](../images/user-guide/create-request.png)

De **[!UICONTROL Create Request]** wordt geopend, met daarin de beschikbare opties voor het indienen van een aanvraag voor een privacytaak voor het momenteel geselecteerde regulatietype.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Selecteer **[!UICONTROL Job Type]** van de aanvraag (&quot;Delete&quot; of &quot;Access&quot;) en een of meer beschikbare producten uit de lijst.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Onder **[!UICONTROL Namespace type]** selecteert u het juiste naamruimtetype voor de klant-id&#39;s waarnaar wordt verzonden [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Als u het standaardnaamruimtetype gebruikt, selecteert u een naamruimte in het keuzemenu (e-mail, ECID of AID) en typt u vervolgens de id-waarden in het tekstvak rechts, door op **\&lt;enter>** voor elke id om deze aan de lijst toe te voegen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Wanneer u het aangepaste naamruimtetype gebruikt, moet u de naamruimte handmatig typen voordat u de onderstaande id-waarden opgeeft.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Als u klaar bent, selecteert u **[!UICONTROL Create]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

Het dialoogvenster verdwijnt en de nieuwe taak (of taken) worden samen met de huidige verwerkingsstatus weergegeven in de widget Taakverzoeken.

### Een JSON-bestand uploaden {#json}

Wanneer u complexere aanvragen maakt, zoals aanvragen die meerdere id-typen gebruiken voor elke gegevenssubject die wordt verwerkt, kunt u een aanvraag maken door een JSON-bestand te uploaden.

Selecteer de pijl naast **[!UICONTROL Create Request]**, onder de widget Statusrapport aan de rechterkant van het scherm. Selecteer in de lijst met opties die wordt weergegeven **[!UICONTROL Upload JSON]**.

![Aanmaakopties aanvragen](../images/user-guide/create-options.png)

De **[!UICONTROL Upload JSON]** wordt weergegeven en geeft u een venster waarin u uw JSON-bestand kunt slepen en neerzetten.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Als u geen JSON-bestand hebt om te uploaden, selecteert u **[!UICONTROL Download Adobe-GDPR-Request.json]** om een sjabloon te downloaden dat u kunt vullen op basis van de waarden die u van de betrokkenen hebt verzameld.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Zoek het JSON-bestand op uw computer en sleep het naar het dialoogvenster. Als het uploaden is voltooid, wordt de bestandsnaam weergegeven in het dialoogvenster. U kunt desgewenst meer JSON-bestanden toevoegen door deze naar het dialoogvenster te slepen.

Als u klaar bent, selecteert u **[!UICONTROL Create]**. Het dialoogvenster verdwijnt en de nieuwe taak (of taken) worden samen met de huidige verwerkingsstatus weergegeven in de widget Taakverzoeken.

### Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u de [!DNL Privacy Service] UI om een privacybaan tot stand te brengen, de details van een baan te bekijken en zijn verwerkingsstatus te controleren, en de resultaten te downloaden zodra het heeft voltooid.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Privacy Service] API, gelieve te verwijzen naar [API-handleiding](../api/overview.md).
