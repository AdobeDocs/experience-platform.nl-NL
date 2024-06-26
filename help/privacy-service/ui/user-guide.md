---
keywords: Experience Platform;home;populaire onderwerpen;exporteren;Exporteren
solution: Experience Platform
title: Privacy-taken beheren in de gebruikersinterface van de Privacy Service
description: Leer hoe u de gebruikersinterface van de Privacy Service gebruikt om privacyverzoeken in verschillende Experiencen Cloud te coördineren en te controleren.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 8ba06a5d572310e2822a5b3c9f82ff0721540f69
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 0%

---

# Privacy-taken beheren in de gebruikersinterface van de Privacy Service {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Privacyverzoeken van betrokkenen in acht nemen"
>abstract="<h2>Beschrijving</h2><p>Met Adobe Experience Platform Privacy Service kunt u privacyverzoeken maken en beheren namens klanten die hun persoonsgegevens willen openen of verwijderen in overeenstemming met de wettelijke privacyregels.</p>"

Dit document bevat stappen voor het maken en beheren van privacyverzoeken met de [!DNL Privacy Service] gebruikersinterface.

>[!IMPORTANT]
>
>Privacy Service is alleen bedoeld voor betrokkenen en verzoeken om consumentenrechten. Elk ander gebruik van Privacy Service voor het opschonen of onderhouden van gegevens wordt niet ondersteund of toegestaan. Adobe is wettelijk verplicht deze tijdig te vervullen. Als zodanig is het testen van belasting op Privacy Service niet toegestaan, omdat dit een productieomgeving is en een onnodige achterstand oplevert bij geldige privacyverzoeken.
>
>Er is nu een vaste uploadlimiet voor dagelijks gebruik om misbruik van de service te voorkomen. Gebruikers die misbruik van het systeem kunnen maken, hebben toegang tot de service uitgeschakeld. Daarna zal er een vergadering met hen worden gehouden om hun acties te bespreken en te bespreken of Privacy Service aanvaardbaar is.

## Bladeren in het dialoogvenster [!DNL Privacy Service] UI-dashboard

Het dashboard voor de [!DNL Privacy Service] De gebruikersinterface bevat twee widgets waarmee u de status van uw privacytaken kunt weergeven: &quot;[!UICONTROL Status Report]&quot; en &quot;[!UICONTROL Job Requests]&quot;. Op het dashboard wordt ook de huidige geselecteerde regelgeving voor de weergegeven taken weergegeven.

![UI-dashboard](../images/user-guide/dashboard.png)

### Type verordening

[!DNL Privacy Service] ondersteunt aanvragen voor een baan voor verschillende privacyregels. In de volgende tabel worden de ondersteunde verordeningen en het bijbehorende label weergegeven, zoals weergegeven in de gebruikersinterface:

| UI-label | Verordening |
| --- | --- |
| [!UICONTROL APA_AUS] | De [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | De [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | De [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | De [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | De [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL GDPR] | De [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_AUS] | De [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | Brazilië [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA] | De [!DNL Washington My Health My Data Act] |
| [!UICONTROL NZPA_NZL] | Nieuw-Zeeland [!DNL Privacy Act] |
| [!UICONTROL PDPA_THA] | Thailand [!DNL Personal Data Protection Act] |
| [!UICONTROL UCPA] | De [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | De [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!--Not released yet:
| [!UICONTROL PDPA_VNM] | Vietnam's [!DNL Personal Data Protection Decree] |
 -->

>[!NOTE]
>
>Zie het overzicht op [ondersteunde privacyregels](../regulations/overview.md) voor meer informatie over de juridische context van elke verordening.

Taken voor elk type regelgeving worden afzonderlijk bijgehouden. Als u wilt schakelen tussen regelgevingstypen, selecteert u de optie **[!UICONTROL Regulation Type]** en selecteer de gewenste verordening in de lijst.

![De console van de Privacy Service met de drop-down van het Type van Reglement.](../images/user-guide/regulation.png)

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
>Wanneer een filter is toegepast op de widget Taakverzoeken, kunt u het filter verwijderen door het **X** op de filterpil. De Verzoeken van de baan keren dan aan de standaard het volgen lijst terug.

### Taakverzoeken {#job-requests}

De [!UICONTROL Job Requests] in de werkruimte vindt u details over de recente taakaanvragen in uw organisatie. De details omvatten het verzoektype, de huidige status, de vervaldatum, de aanvrager e-mail, etc. Sets van 100 records worden tegelijk geladen. Standaard worden de laatst gemaakte taken bovenaan weergegeven met meer records die zijn geladen wanneer u omlaag schuift om te bladeren.

>[!NOTE]
>
>De gegevens voor eerder gecreëerde banen zijn slechts 30 dagen na de voltooiingsdatum toegankelijk.

U kunt de lijst filteren door trefwoorden in de zoekbalk onder de knop [!UICONTROL Job Requests] titel. De lijst filtert automatisch terwijl u typt, tonend verzoeken die waarden bevatten die uw onderzoekstermijnen aanpassen. Het zoekveld voert een &#39;snelle&#39; zoekopdracht uit die overeenkomt met de privacytaak-id&#39;s van de taken die momenteel zijn gerenderd of geladen in de gebruikersinterface. Het is geen uitgebreide zoekopdracht naar al uw ingediende taken. Het is eerder een filter dat op de geladen resultaten wordt toegepast. Gebruik de Privacy Service-API om [retourbanen op basis van een specifieke verordening, een datumbereik of een enkele baan](../api/privacy-jobs.md#list).

>[!TIP]
>
>Als u records vanaf de afgelopen 30 dagen in de gebruikersinterface wilt laden, moet u naar beneden schuiven en meer batches records laden.

![Het gedeelte Aanvraag voor privacyconsole met het zoekveld gemarkeerd.](../images/user-guide/job-search.png)

U kunt ook de zoekknop gebruiken om een query voor een privacytaak uit te voeren die een bepaald datumbereik omvat. Deze actie retourneert alle privacytaken die door uw organisatie tijdens de opgegeven tijdsperiode zijn ingediend. Selecteer de **[!UICONTROL Requested on]** vervolgkeuzemenu om een begin- en einddatum voor de query te kiezen. Tot de beschikbare opties behoren [!UICONTROL Today], [!UICONTROL Last 7 Days], [!UICONTROL Last 2 Weeks], [!UICONTROL Last 30 Days], of [!UICONTROL Custom]. Indien gebruikt met de [!UICONTROL Requested on] in de zoekfunctie worden alleen taakaanvragen weergegeven die tussen de door u gekozen datumbereiken zijn verzonden.

![De sectie Taakverzoek met het zoekveld, Gevraagd in het vervolgkeuzemenu en de knop Zoeken gemarkeerd.](../images/user-guide/requested-on-dropdown-menu.png)

Als u de details van een bepaalde taakaanvraag wilt bekijken, selecteert u de taak-id van de aanvraag in de lijst om de opdracht **[!UICONTROL Job Details]** pagina.

![Taakgegevens GDPR-interface](../images/user-guide/job-details.png)

Dit dialoogvenster bevat statusinformatie over elk [!DNL Experience Cloud] oplossing en de huidige toestand in verhouding tot de algemene taak. Aangezien elke privacybaan asynchroon is, toont de pagina de recentste communicatie datum en tijd (GMT) van elke oplossing, aangezien sommige meer tijd dan anderen vereisen om het verzoek te verwerken.

Als een oplossing om het even welke extra gegevens heeft verstrekt, is het viewable in deze dialoog. U kunt deze gegevens weergeven door afzonderlijke productrijen te selecteren.

Selecteer **[!UICONTROL Export to CSV]** rechtsboven in het dialoogvenster.

## Een nieuw verzoek voor een privacytaak maken {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Instructies"
>abstract="<ul><li>Selecteren <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">Verzoeken</a> in de linkernavigatie om Ul van de Privacy te openen, dan uitgezocht <b>Aanvraag maken</b>.</li><li>Vanaf hier kunt u de aanvraagbuilder gebruiken of een JSON-bestand van betrokkenen uploaden.</li><li>Als u de aanvraagbuilder gebruikt, selecteert u het taaktype (toegang en/of verwijderen) en kiest u het type identiteit dat u opgeeft (e-mail, ECID of AID), of voert u een naamruimte voor een aangepaste identiteit in. Voer de juiste identiteitswaarden voor de klanten in en selecteer <b>Maken</b> wanneer gereed.</li><li>Als u een JSON-bestand uploadt, selecteert u de pijl naast Verzoek maken. Selecteer in de lijst met opties de optie <b>JSON uploaden</b> en uploadt u het bestand. Als u geen JSON-bestand hebt om te uploaden, selecteert u <b>Download Adobe-GDPR-Request.json</b> om een sjabloon te downloaden dat u kunt vullen. Upload JSON en selecteer <b>Maken</b> wanneer gereed.</li><li>Raadpleeg voor meer informatie over deze functie de <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html">Gebruikershandleiding voor Privacy Service</a> op Experience League.</li></ul>"

>[!NOTE]
>
>Als u een privacytaakverzoek wilt maken, moet u identiteitsgegevens opgeven voor de specifieke klanten van wie de gegevens moeten worden benaderd of verwijderd. Controleer het document op [identiteitsgegevens voor privacyverzoeken](../identity-data.md) voordat u doorgaat met deze sectie.

De [!DNL Privacy Service] UI biedt twee methoden om nieuwe taakaanvragen te maken:

* [De Request Builder gebruiken](#request-builder)
* [Een JSON-bestand uploaden](#json)

De stappen voor het gebruiken van elk van deze methodes worden verstrekt in de volgende secties.

### De Request Builder gebruiken {#request-builder}

Met de Request Builder kunt u handmatig een nieuw verzoek voor een privacytaak maken in de gebruikersinterface. De Bouwer van het Verzoek wordt best gebruikt voor eenvoudigere en kleinere reeksen verzoeken, omdat de de grensverzoeken van de Bouwer van het Verzoek om slechts identiteitskaart type per gebruiker te hebben. Voor meer gecompliceerde verzoeken kan het beter zijn [een JSON-bestand uploaden](#json) in plaats daarvan.

Selecteer **[!UICONTROL Create Request]** onder de widget Statusrapport rechts op het scherm.

![Aanvraag maken selecteren](../images/user-guide/create-request.png)

De **[!UICONTROL Create Request]** wordt geopend, met daarin de beschikbare opties voor het indienen van een aanvraag voor een privacytaak voor het momenteel geselecteerde regulatietype.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Selecteer de **[!UICONTROL Job Type]** van de aanvraag (&quot;Delete&quot; of &quot;Access&quot;) en een of meer beschikbare producten uit de lijst.

Privacy Service ondersteunt twee soorten verzoeken om persoonlijke gegevens: [!UICONTROL Access] (lezen) en/of [!UICONTROL Delete]. U kunt een verzoek indienen om alle informatie in het product te ontvangen die betrekking heeft op het onderwerp van het onderzoek, of u kunt verzoeken om alle informatie te schrappen die betrekking heeft op het onderwerp van het onderzoek.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Onder **[!UICONTROL Namespace type]** selecteert u het juiste naamruimtetype voor de klant-id&#39;s waarnaar wordt verzonden [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Als u het standaardnaamruimtetype gebruikt, selecteert u een naamruimte in het keuzemenu (e-mail, ECID of AID) en typt u vervolgens de id-waarden in het tekstvak rechts, door op **\&lt;enter>** voor elke id om deze aan de lijst toe te voegen.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Wanneer u het aangepaste naamruimtetype gebruikt, moet u de naamruimte handmatig typen voordat u de onderstaande id-waarden opgeeft.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Selecteer **[!UICONTROL Create]**.

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

Selecteer **[!UICONTROL Create]**. Het dialoogvenster verdwijnt en de nieuwe taak (of taken) worden samen met de huidige verwerkingsstatus weergegeven in de widget Taakverzoeken.

### Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u de [!DNL Privacy Service] UI om een privacybaan tot stand te brengen, de details van een baan te bekijken en zijn verwerkingsstatus te controleren, en de resultaten te downloaden zodra het heeft voltooid.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Privacy Service] API, gelieve te verwijzen naar [API-handleiding](../api/overview.md).
