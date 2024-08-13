---
title: Sandbox Tooling
description: U kunt Sandboxconfiguraties naadloos exporteren en importeren tussen sandboxen.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: ac013f4a1b0f8053963771b66d0bd80111f7d215
workflow-type: tm+mt
source-wordcount: '2147'
ht-degree: 0%

---

# Gereedschap Sandbox

>[!NOTE]
>
>Gereedschap voor sandboxen is een basisfunctie die zowel [!DNL Real-Time Customer Data Platform] als [!DNL Journey Optimizer] ondersteunt om de efficiëntie van de ontwikkelingscyclus en de nauwkeurigheid van de configuratie te verbeteren.<br><br> u wordt vereist om de volgende twee op rol-gebaseerde toegangsbeheertoestemmingen te hebben om de zandbaktooling eigenschap te gebruiken:<br> - `manage-sandbox` of `view-sandbox`<br> - `manage-package`

Verbeter de configuratienauwkeurigheid over sandboxen en voer naadloos sandboxconfiguraties tussen sandboxen in met de functie voor het bewerken van sandboxen. Gebruik de gereedheid van de sandbox om de tijd die nodig is voor het implementatieproces te verkorten en geslaagde configuraties over de sandboxen te verplaatsen.

U kunt de functie voor gereedschappen in de sandbox gebruiken om verschillende objecten te selecteren en deze te exporteren naar een pakket. Een pakket kan uit één object of uit meerdere objecten bestaan. <!--or an entire sandbox.--> om het even welke voorwerpen die in een pakket inbegrepen zijn moeten van de zelfde zandbak zijn.

## Objecten ondersteund voor gereedmaken van sandbox {#supported-objects}

Met de functie voor het gereedmaken van de sandbox kunt u [!DNL Adobe Real-Time Customer Data Platform] - en [!DNL Adobe Journey Optimizer] -objecten exporteren naar een pakket.

### Real-time Customer Data Platform-objecten {#real-time-cdp-objects}

De onderstaande tabel bevat een lijst met [!DNL Adobe Real-Time Customer Data Platform] -objecten die momenteel worden ondersteund voor gereedschappen in sandboxen:

| Platform | Object | Details |
| --- | --- | --- |
| Klantgegevensplatform | Bronnen | De referenties van de bronaccount worden om beveiligingsredenen niet gerepliceerd in de doelsandbox en moeten handmatig worden bijgewerkt. De brongegevensstroom wordt standaard gekopieerd in een conceptstatus. |
| Klantgegevensplatform | Doelgroepen | Alleen het **[!UICONTROL Customer Audience]** type **[!UICONTROL Segmentation service]** wordt ondersteund. Bestaande labels voor toestemming en bestuur worden in dezelfde importtaak gekopieerd. Het systeem zal automatisch het Standaard Beleid van de Fusie in doelzandbak met de zelfde klasse selecteren XDM wanneer het controleren van de gebiedsdelen van het fusiebeleid. |
| Klantgegevensplatform | Identiteiten | Het systeem dedupliceert standaard identiteitsnaamruimten voor Adoben automatisch wanneer u deze maakt in de doelsandbox. Het publiek kan slechts worden gekopieerd wanneer alle attributen in publieksregels in het unieschema worden toegelaten. De noodzakelijke schema&#39;s moeten eerst voor verenigd profiel worden bewogen en worden toegelaten. |
| Klantgegevensplatform | Schema&#39;s | Bestaande labels voor toestemming en bestuur worden in dezelfde importtaak gekopieerd. De gebruiker heeft de flexibiliteit om schema&#39;s in te voeren zonder de Verenigde toegelaten optie van het Profiel. Het randgeval van de schema-relaties wordt niet opgenomen in het pakket. |
| Klantgegevensplatform | Gegevenssets | Datasets worden gekopieerd met de instelling voor het uniforme profiel standaard uitgeschakeld. |
| Klantgegevensplatform | Beleid inzake instemming en bestuur | Voeg aangepast beleid dat door een gebruiker is gemaakt, toe aan een pakket en verplaats het naar andere sandboxen. |

De volgende objecten worden geïmporteerd, maar hebben een concept- of een uitgeschakelde status:

| Functie | Object | Status |
| --- | --- | --- |
| Importstatus | Source-dataflow | Concept |
| Importstatus | Reis | Concept |
| Verenigd profiel | Gegevensset | Verenigd profiel uitgeschakeld |
| Beleid | Beleid inzake gegevensbeheer | Uitgeschakeld |

### Adobe Journey Optimizer-objecten {#abobe-journey-optimizer-objects}

De onderstaande tabel bevat een lijst met [!DNL Adobe Journey Optimizer] -objecten die momenteel worden ondersteund voor het gebruik van sandboxgereedschappen en beperkingen:

| Platform | Object | Details |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Doelgroep | Een publiek kan als afhankelijk voorwerp van het reisvoorwerp worden gekopieerd. U kunt een nieuw publiek maken of een bestaand publiek in de doelsandbox opnieuw gebruiken. |
| [!DNL Adobe Journey Optimizer] | Schema | De schema&#39;s die in de reis worden gebruikt kunnen als afhankelijke voorwerpen worden gekopieerd. U kunt een nieuw schema selecteren of een bestaand schema in de doelzandbak opnieuw gebruiken. |
| [!DNL Adobe Journey Optimizer] | Samenvoegbeleid | Het samenvoegbeleid dat in de reis wordt gebruikt, kan als afhankelijke voorwerpen worden gekopieerd. In de doelzandbak, kunt u **niet** een nieuw fusiebeleid tot stand brengen, kunt u reeds bestaande slechts gebruiken. |
| [!DNL Adobe Journey Optimizer] | Reis - canvasdetails | De representatie van de reis op het canvas omvat de objecten in de reis, zoals voorwaarden, handelingen, gebeurtenissen, leestekens, enzovoort, die worden gekopieerd. De sprongactiviteit wordt uitgesloten van het exemplaar. |
| [!DNL Adobe Journey Optimizer] | Gebeurtenis | De gebeurtenissen en gebeurtenisdetails die in de reis worden gebruikt worden gekopieerd. Er wordt altijd een nieuwe versie gemaakt in de doelsandbox. |
| [!DNL Adobe Journey Optimizer] | Actie | E-mail- en pushberichten die tijdens de rit worden gebruikt, kunnen als afhankelijke objecten worden gekopieerd. De activiteiten van de kanaalactie die op de reisgebieden worden gebruikt, die voor verpersoonlijking in het bericht worden gebruikt, worden niet gecontroleerd op volledigheid. Inhoudsblokken worden niet gekopieerd.<br><br> de actie van het updateprofiel die in de reis wordt gebruikt kan worden gekopieerd. De acties en de actiedetails van de douane die in de reis worden gebruikt worden ook gekopieerd. Er wordt altijd een nieuwe versie gemaakt in de doelsandbox. |

Oppervlakken (bijvoorbeeld voorinstellingen) worden niet overschreven. Het systeem selecteert automatisch de dichtstbijzijnde mogelijke overeenkomst op de bestemmingszandbak die op het berichttype en oppervlaknaam wordt gebaseerd. Als er geen oppervlakten op de doelzandbak worden gevonden, dan zal het oppervlakexemplaar ontbreken, veroorzakend het berichtexemplaar om te ontbreken omdat een bericht vereist een oppervlakte om voor opstelling beschikbaar te zijn. In dit geval moet ten minste één oppervlak worden gemaakt voor het rechterkanaal van het bericht, zodat de kopie kan werken.

Aangepaste identiteitstypen worden niet ondersteund als afhankelijke objecten wanneer u een reis exporteert.

## Objecten exporteren naar een pakket {#export-objects}

>[!NOTE]
>
>Alle uitvoeracties worden in de auditlogboeken opgenomen.

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Een object verwijderen"
>abstract="Als u een object uit het pakket wilt verwijderen, selecteert u de rij die u wilt verwijderen en gebruikt u vervolgens de verwijderoptie die bij de selectie beschikbaar wordt gemaakt. U kunt geen objecten verwijderen uit gepubliceerde pakketten."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Vervalinstellingen van pakket"
>abstract="Pakketten verlopen na een periode van inactiviteit in de status van het concept. De standaarddatum is ingesteld op 90 dagen vanaf vandaag. Deze datum blijft wijzigen totdat het pakket is gepubliceerd. Als u het pakket morgen als concept-status bezoekt, wordt de datum met +1 dag verplaatst, tenzij u dit handmatig instelt."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Pakketstatus"
>abstract="Standaard is de status ingesteld op concept. Nadat het pakket is gepubliceerd, wordt de status gewijzigd in gepubliceerd. Er kunnen geen wijzigingen worden aangebracht nadat het pakket is gepubliceerd."

>[!NOTE]
>
>U kunt een pakket alleen importeren als u toegangsrechten hebt voor de objecten.

In dit voorbeeld wordt het exporteren van een schema en het toevoegen aan een pakket gedocumenteerd. U kunt het zelfde proces gebruiken om andere voorwerpen, bijvoorbeeld, datasets, reizen, en vele anderen uit te voeren.

### Object toevoegen aan een nieuw pakket {#add-object-to-new-package}

Selecteer **[!UICONTROL Schemas]** in de linkernavigatie en selecteer vervolgens het tabblad **[!UICONTROL Browse]** , waarin de beschikbare schema&#39;s worden vermeld. Selecteer vervolgens de ellips (`...`) naast het geselecteerde schema en een vervolgkeuzelijst met besturingselementen. Selecteer **[!UICONTROL Add to package]** in de vervolgkeuzelijst.

![ Lijst van schema&#39;s die het dropdown menu tonen dat de [!UICONTROL Add to package] controle benadrukt.](../images/ui/sandbox-tooling/add-to-package.png)

Selecteer de optie **[!UICONTROL Create new package]** in het dialoogvenster **[!UICONTROL Add to package]** . Geef een [!UICONTROL Name] voor het pakket op en een optioneel [!UICONTROL Description] en selecteer vervolgens **[!UICONTROL Add]** .

![ de [!UICONTROL Add to package] dialoog met [!UICONTROL Create new package] geselecteerd en het benadrukken [!UICONTROL Add].](../images/ui/sandbox-tooling/create-new-package.png)

U wordt teruggestuurd naar de **[!UICONTROL Schemas]** -omgeving. U kunt nu extra objecten toevoegen aan het pakket dat u hebt gemaakt door de volgende stappen hieronder uit te voeren.

### Een object toevoegen aan een bestaand pakket en publiceren {#add-object-to-existing-package}

Als u een lijst met beschikbare schema&#39;s wilt weergeven, selecteert u **[!UICONTROL Schemas]** in de linkernavigatie en selecteert u vervolgens de tab **[!UICONTROL Browse]** . Selecteer vervolgens de ellips (`...`) naast het geselecteerde schema om de besturingsopties in een vervolgkeuzemenu weer te geven. Selecteer **[!UICONTROL Add to package]** in de vervolgkeuzelijst.

![ Lijst van schema&#39;s die het dropdown menu tonen dat de [!UICONTROL Add to package] controle benadrukt.](../images/ui/sandbox-tooling/add-to-package.png)

Het dialoogvenster **[!UICONTROL Add to package]** wordt weergegeven. Selecteer de optie **[!UICONTROL Existing package]** , selecteer vervolgens het vervolgkeuzemenu **[!UICONTROL Package name]** en selecteer het vereiste pakket. Selecteer ten slotte **[!UICONTROL Add]** om uw keuzes te bevestigen.

![[!UICONTROL Add to package] , waarin een geselecteerd pakket uit het vervolgkeuzemenu wordt weergegeven. ](../images/ui/sandbox-tooling/add-to-existing-package.png)

De lijst met objecten die aan het pakket zijn toegevoegd, wordt weergegeven. Selecteer **[!UICONTROL Publish]** als u het pakket wilt publiceren en het beschikbaar wilt maken voor import in sandboxen.

![ een lijst van voorwerpen in het pakket, die de [!UICONTROL Publish] optie benadrukken.](../images/ui/sandbox-tooling/publish-package.png)

Selecteer **[!UICONTROL Publish]** om de publicatie van het pakket te bevestigen.

![ de dialoog van de het pakketbevestiging van Publish, die de [!UICONTROL Publish] optie benadrukt.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Nadat het pakket is gepubliceerd, kan de inhoud ervan niet meer worden gewijzigd. Om compatibiliteitsproblemen te voorkomen, moet u ervoor zorgen dat alle benodigde middelen zijn geselecteerd. Als er wijzigingen moeten worden aangebracht, moet u een nieuw pakket maken.

U keert terug naar het tabblad **[!UICONTROL Packages]** in de [!UICONTROL Sandboxes] -omgeving, waar u het nieuwe gepubliceerde pakket kunt zien.

![ Lijst van zandbakpakketten die het nieuwe gepubliceerde pakket benadrukken.](../images/ui/sandbox-tooling/published-packages.png)

## Een pakket importeren naar een doelsandbox {#import-package-to-target-sandbox}

>[!NOTE]
>
>Alle importacties worden vastgelegd in de auditlogboeken.

Als u het pakket in een doelsandbox wilt importeren, navigeert u naar het tabblad Sandboxen **[!UICONTROL Browse]** en selecteert u de plusoptie (+) naast de naam van de sandbox.

![ de zandbakken **[!UICONTROL Browse]** lusje die de het invoerpakketselectie benadrukken.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Selecteer in het vervolgkeuzemenu de **[!UICONTROL Package name]** die u wilt importeren in de doelsandbox. Voeg een **[!UICONTROL Job name]** toe die wordt gebruikt voor toekomstige controle. Standaard wordt het uniforme profiel uitgeschakeld wanneer de schema&#39;s van het pakket worden geïmporteerd. Wissel **toe laat schema&#39;s voor profiel** om dit toe te laten, dan selecteren **[!UICONTROL Next]**.

![ de pagina van de invoerdetails die de [!UICONTROL Package name] dropdown selectie ](../images/ui/sandbox-tooling/import-package-to-sandbox.png) toont

De pagina [!UICONTROL Package object and dependencies] bevat een lijst met alle elementen in dit pakket. Het systeem detecteert automatisch afhankelijke objecten die nodig zijn om geselecteerde bovenliggende objecten te kunnen importeren. Alle ontbrekende kenmerken worden boven aan de pagina weergegeven. Selecteer **[!UICONTROL View details]** voor een meer gedetailleerde uitsplitsing.

![ de [!UICONTROL Package object and dependencies] pagina toont ontbrekende attributen.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Afhankelijke objecten kunnen worden vervangen door bestaande objecten in de doelsandbox, zodat u bestaande objecten opnieuw kunt gebruiken in plaats van een nieuwe versie te maken. Wanneer u bijvoorbeeld een pakket met schema&#39;s importeert, kunt u de bestaande aangepaste veldgroep en naamruimten in de doelsandbox opnieuw gebruiken. U kunt ook bestaande segmenten in de doelsandbox opnieuw gebruiken wanneer u een pakket importeert, inclusief de stappen voor reizen.

Als u een bestaand object wilt gebruiken, selecteert u het potloodpictogram naast het afhankelijke object.

![ de [!UICONTROL Package object and dependencies] pagina toont een lijst van activa inbegrepen in het pakket.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

De opties voor het maken van nieuwe of het gebruik van bestaande bestanden worden weergegeven. Selecteer **[!UICONTROL Use existing]**.

![ de [!UICONTROL Package object and dependencies] pagina die afhankelijke objecten opties [!UICONTROL Create new] en [!UICONTROL Use existing] tonen.](../images/ui/sandbox-tooling/use-existing-object.png)

Het dialoogvenster **[!UICONTROL Field group]** bevat een lijst met veldgroepen die beschikbaar zijn voor het object. Selecteer de gewenste veldgroepen en selecteer vervolgens **[!UICONTROL Save]** .

![ een lijst van gebieden die op de [!UICONTROL Field group] dialoog worden getoond, die de [!UICONTROL Save] selectie benadrukken. ](../images/ui/sandbox-tooling/field-group-list.png)

U wordt teruggestuurd naar de pagina [!UICONTROL Package object and dependencies] . Selecteer van hieruit **[!UICONTROL Finish]** om het importeren van het pakket te voltooien.

![ de [!UICONTROL Package object and dependencies] pagina toont een lijst van activa inbegrepen in het pakket, benadrukkend [!UICONTROL Finish].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Een volledige sandbox exporteren en importeren

>[!NOTE]
>
>Momenteel worden alleen Real-time Customer Data Platform-objecten ondersteund bij het exporteren of importeren van een volledige sandbox. Adobe Journey Optimizer-objecten zoals reizen worden momenteel niet ondersteund.

U kunt alle ondersteunde objecttypen exporteren naar een volledig sandboxpakket en het pakket vervolgens in verschillende sandboxen importeren om objectconfiguraties te repliceren. Met deze functionaliteit kunt u bijvoorbeeld:

- Importeer een sandbox opnieuw om alle objectconfiguraties te reproduceren als u de sandbox opnieuw moet instellen
- Importeer het pakket in andere sandboxen en gebruik het als een blauwdruksandbox om het ontwikkelingsproces te versnellen.

### Een volledige sandbox exporteren {#export-entire-sandbox}

Als u een volledige sandbox wilt exporteren, navigeert u naar de tab [!UICONTROL Sandboxes] **[!UICONTROL Packages]** en selecteert u **[!UICONTROL Create package]** .

![ het [!UICONTROL Sandboxes] **[!UICONTROL Packages]** lusje benadrukken [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Selecteer **[!UICONTROL Entire sandbox]** voor [!UICONTROL Type of package] in het dialoogvenster [!UICONTROL Create package] . Geef een [!UICONTROL Package name] op voor het nieuwe pakket en selecteer de **[!UICONTROL Sandbox]** in het vervolgkeuzemenu. Selecteer ten slotte **[!UICONTROL Create]** om uw gegevens te bevestigen.

![ de dialoog die [!UICONTROL Create package] voltooide gebieden toont en [!UICONTROL Create] benadrukt.](../images/ui/sandbox-tooling/create-package-dialog.png)

Het pakket is gemaakt en selecteer **[!UICONTROL Publish]** om het pakket te publiceren.

![ Lijst van zandbakpakketten die het nieuwe gepubliceerde pakket benadrukken.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

U keert terug naar het tabblad **[!UICONTROL Packages]** in de [!UICONTROL Sandboxes] -omgeving, waar u het nieuwe gepubliceerde pakket kunt zien.

### Het volledige sandboxpakket importeren {#import-entire-sandbox-package}

>[!NOTE]
>
>Alle objecten worden als nieuwe objecten geïmporteerd in de doelsandbox. Het wordt aanbevolen een volledig sandboxpakket te importeren in een lege sandbox.

Als u het pakket in een doelsandbox wilt importeren, navigeert u naar het tabblad [!UICONTROL Sandboxes] **[!UICONTROL Browse]** en selecteert u de optie met het plusteken (+) naast de naam van de sandbox.

![ de zandbakken **[!UICONTROL Browse]** lusje die de het invoerpakketselectie benadrukken.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Selecteer de volledige sandbox met behulp van het vervolgkeuzemenu **[!UICONTROL Package name]** . Voeg een **[!UICONTROL Job name]** toe, die wordt gebruikt voor toekomstige controle en een optioneel **[!UICONTROL Job description]** , en selecteer vervolgens **[!UICONTROL Next]** .

![ de pagina van de invoerdetails die de [!UICONTROL Package name] dropdown selectie ](../images/ui/sandbox-tooling/import-full-sandbox-package.png) toont

>[!NOTE]
>
>U moet volledige machtigingen hebben voor alle objecten die in het pakket zijn opgenomen. Als u geen machtigingen hebt, mislukt het importeren en verschijnen er foutberichten.

U gaat naar de pagina [!UICONTROL Package object and dependencies] waar u het aantal objecten en afhankelijkheden kunt zien die zijn geïmporteerd en uitgesloten. Selecteer van hieruit **[!UICONTROL Import]** om het importeren van het pakket te voltooien.

![ de [!UICONTROL Package object and dependencies] pagina toont het gealigneerde bericht van objecten types niet gesteund, benadrukkend [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Zorg ervoor dat de importbewerking enige tijd duurt. De tijd die nodig is om te voltooien, is afhankelijk van het aantal objecten in het pakket. U kunt de importtaak controleren vanaf het tabblad [!UICONTROL Sandboxes] **[!UICONTROL Jobs]** .

## Importdetails controleren {#view-import-details}

Als u de geïmporteerde details wilt weergeven, navigeert u naar het tabblad [!UICONTROL Sandboxes] **[!UICONTROL Jobs]** en selecteert u het pakket in de lijst. U kunt ook de zoekbalk gebruiken om naar het pakket te zoeken.

![ het lusje van zandbakken [!UICONTROL Jobs] benadrukt de het invoerpakketselectie.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Selecteer **[!UICONTROL View import summary]** in het rechterdetailvenster op het tabblad **[!UICONTROL Jobs]** in de Sandboxomgeving.

![ het zandbakken [!UICONTROL Imports] lusje benadrukt de [!UICONTROL View import details] selectie in de juiste ruit.](../images/ui/sandbox-tooling/view-import-details.png)

In het dialoogvenster **[!UICONTROL Import summary]** wordt een percentage weergegeven van de importbewerkingen.

>[!NOTE]
>
>U kunt een lijst met objecten weergeven door naar specifieke overzichtspagina&#39;s te navigeren.

![ de dialoog die [!UICONTROL Import details] een gedetailleerde uitsplitsing van de invoer toont.](../images/ui/sandbox-tooling/import-details.png)

Wanneer de importbewerking is voltooid, ontvangt u een melding in de gebruikersinterface van het platform. U kunt deze meldingen openen via het waarschuwingspictogram. U kunt hier naar probleemoplossing navigeren als een taak mislukt.

## Videotutorial

De volgende video is bedoeld ter ondersteuning van uw begrip van gereedschappen voor sandboxen en beschrijft hoe u een nieuw pakket kunt maken, een pakket kunt publiceren en importeren.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Volgende stappen

In dit document wordt getoond hoe u de functie voor het gereedmaken van de sandbox in de gebruikersinterface van het Experience Platform kunt gebruiken. Voor informatie over zandbakken, zie de [ gids van de zandbakgebruiker ](../ui/user-guide.md).

Voor stappen bij het uitvoeren van verschillende verrichtingen die Sandbox API gebruiken, zie de [ gids van de zandbakontwikkelaar ](../api/getting-started.md). Voor een overzicht op hoog niveau van zandbakken in Experience Platform, verwijs naar de [ overzichtsdocumentatie ](../home.md).
