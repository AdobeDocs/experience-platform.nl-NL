---
title: Sandboxen
description: U kunt Sandboxconfiguraties naadloos exporteren en importeren tussen sandboxen.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 0aaba1d1ae47908ea92e402b284438accb4b4731
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# [!BADGE Beta] Gereedschap Sandbox

>[!IMPORTANT]
>
>De **Gereedschap Sandbox** hieronder beschreven functie is alleen beschikbaar voor het selecteren van bètaklanten.

>[!NOTE]
>
>Gereedschap voor sandboxen is een basisfunctie die beide ondersteunt [!DNL Real-Time Customer Data Platform] en [!DNL Journey Optimizer] verbetering van de efficiëntie van de ontwikkelingscyclus en de nauwkeurigheid van de configuratie.<br><br>U moet de volgende twee op rol-gebaseerde toegangsbeheertoestemmingen hebben om de zandbaktoolingeigenschap te gebruiken:<br>- `manage-sandbox` of `view-sandbox`<br>- `manage-package`

Verbeter de configuratienauwkeurigheid over sandboxen en voer naadloos sandboxconfiguraties tussen sandboxen in met de functie voor het bewerken van sandboxen. Gebruik de gereedheid van de sandbox om de tijd die nodig is voor het implementatieproces te verkorten en geslaagde configuraties over de sandboxen te verplaatsen.

U kunt de functie voor gereedschappen in de sandbox gebruiken om verschillende objecten te selecteren en deze te exporteren naar een pakket. Een pakket kan uit één object of uit meerdere objecten bestaan. <!--or an entire sandbox.-->Alle objecten die in een pakket zijn opgenomen, moeten afkomstig zijn uit dezelfde sandbox.

## Objecten ondersteund voor gereedmaken van sandbox {#supported-objects}

Met de functie voor het gereedschap Sandbox kunt u exporteren [!DNL Adobe Real-Time Customer Data Platform] en [!DNL Adobe Journey Optimizer] objecten in een pakket plaatsen.

### Real-time Customer Data Platform-objecten {#real-time-cdp-objects}

De onderstaande tabel bevat [!DNL Adobe Real-Time Customer Data Platform] objecten die momenteel worden ondersteund voor gereedschappen in sandbox:

| Platform | Object | Details |
| --- | --- | --- |
| Klantgegevensplatform | Bronnen | De referenties van de bronaccount worden om beveiligingsredenen niet gerepliceerd in de doelsandbox en moeten handmatig worden bijgewerkt. De brongegevensstroom wordt standaard gekopieerd in een conceptstatus. |
| Klantgegevensplatform | Doelgroepen | Alleen de **[!UICONTROL Customer Audience]** type **[!UICONTROL Segmentation service]** wordt ondersteund. Bestaande labels voor toestemming en bestuur worden in dezelfde importtaak gekopieerd. |
| Klantgegevensplatform | Identiteiten | Het systeem dedupliceert standaard identiteitsnaamruimten voor Adoben automatisch wanneer u deze maakt in de doelsandbox. Het publiek kan slechts worden gekopieerd wanneer alle attributen in publieksregels in het unieschema worden toegelaten. De noodzakelijke schema&#39;s moeten eerst voor verenigd profiel worden bewogen en worden toegelaten. |
| Klantgegevensplatform | Schema&#39;s | Bestaande labels voor toestemming en bestuur worden in dezelfde importtaak gekopieerd. De schema verenigde profielstatus wordt gekopieerd zoals deze van de bronzandbak is. Als het schema voor één profiel in de bronzandbak wordt toegelaten, worden alle attributen verplaatst naar het unieschema. Het randgeval van de schema-relaties wordt niet opgenomen in het pakket. |
| Klantgegevensplatform | Gegevenssets | Datasets worden gekopieerd met de instelling voor het uniforme profiel standaard uitgeschakeld. |

De volgende objecten worden geïmporteerd, maar hebben een concept- of een uitgeschakelde status:

| Functie | Object | Status |
| --- | --- | --- |
| Importstatus | Brongegevensstroom | Concept |
| Importstatus | Reis | Concept |
| Verenigd profiel | Gegevensset | Verenigd profiel uitgeschakeld |
| Beleid | Beleid inzake gegevensbeheer | Uitgeschakeld |

### Adobe Journey Optimizer-objecten {#abobe-journey-optimizer-objects}

De onderstaande tabel bevat [!DNL Adobe Journey Optimizer] objecten die momenteel worden ondersteund voor gereedschappen en beperkingen voor sandboxen:

| Platform | Object | Details |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Audience | Een publiek kan als afhankelijk voorwerp van het reisvoorwerp worden gekopieerd. U kunt een nieuw publiek maken of een bestaand publiek in de doelsandbox opnieuw gebruiken. |
| [!DNL Adobe Journey Optimizer] | Schema | De schema&#39;s die in de reis worden gebruikt kunnen als afhankelijke voorwerpen worden gekopieerd. U kunt een nieuw schema selecteren of een bestaand schema in de doelzandbak opnieuw gebruiken. |
| [!DNL Adobe Journey Optimizer] | Bericht | De berichten die in de reis worden gebruikt kunnen als afhankelijke voorwerpen worden gekopieerd. De activiteiten van de kanaalactie die op de reisgebieden worden gebruikt, die voor verpersoonlijking in het bericht worden gebruikt, worden niet gecontroleerd op volledigheid. Inhoudsblokken worden niet gekopieerd. |
| [!DNL Adobe Journey Optimizer] | Reis - canvasdetails | De representatie van de reis op het canvas omvat de objecten in de reis, zoals voorwaarden, handelingen, gebeurtenissen, leestekens, enzovoort, die worden gekopieerd. De sprongactiviteit wordt uitgesloten van het exemplaar. |
| [!DNL Adobe Journey Optimizer] | Gebeurtenis | De gebeurtenissen en gebeurtenisdetails die in de reis worden gebruikt worden gekopieerd. Er wordt altijd een nieuwe versie gemaakt in de doelsandbox. |
| [!DNL Adobe Journey Optimizer] | Actie | De acties en actiedetails die in de reis worden gebruikt worden gekopieerd. Er wordt altijd een nieuwe versie gemaakt in de doelsandbox. |

Oppervlakken (bijvoorbeeld voorinstellingen) worden niet overschreven. Het systeem selecteert automatisch de dichtstbijzijnde mogelijke overeenkomst op de bestemmingszandbak die op het berichttype en oppervlaknaam wordt gebaseerd. Als er geen oppervlakten op de doelzandbak worden gevonden, dan zal het oppervlakexemplaar ontbreken, veroorzakend het berichtexemplaar om te ontbreken omdat een bericht vereist een oppervlakte om voor opstelling beschikbaar te zijn. In dit geval moet ten minste één oppervlak worden gemaakt voor het rechterkanaal van het bericht, zodat de kopie kan werken.

Aangepaste identiteitstypen worden niet ondersteund als afhankelijke objecten wanneer u een reis exporteert.

## Objecten exporteren naar een pakket {#export-objects}

>[!NOTE]
>
>Alle uitvoeracties worden in de auditlogboeken opgenomen.

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="Pakket opslaan en afsluiten"
>abstract="Als u het pakket wilt afsluiten en opslaan, kunnen gebruikers gewoon de optie Vorige gebruiken."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Een object verwijderen"
>abstract="De gebruiker moet de rij selecteren en vervolgens de rij verwijderen met de verwijderoptie (beschikbaar gemaakt bij selectie)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Vervalinstellingen van pakket"
>abstract="De datum is vastgesteld op 90 dagen vanaf vandaag. Deze datum blijft wijzigen totdat het pakket is gepubliceerd. Als een gebruiker het pakket morgen als concept-status bezoekt, wordt de datum met +1 dag verplaatst (tenzij de gebruiker dit heeft ingesteld)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Pakketstatus"
>abstract="Standaard is de status ingesteld op concept. Nadat het pakket is gepubliceerd, wordt de status gewijzigd in gepubliceerd. Er kunnen geen wijzigingen worden aangebracht nadat het pakket is gepubliceerd."

>[!NOTE]
>
>U kunt een pakket alleen importeren als u toegangsrechten hebt voor de objecten.

In dit voorbeeld wordt het exporteren van een schema en het toevoegen aan een pakket gedocumenteerd. U kunt het zelfde proces gebruiken om andere voorwerpen, bijvoorbeeld, datasets, reizen, en vele anderen uit te voeren.

### Object toevoegen aan een nieuw pakket {#add-object-to-new-package}

Selecteren **[!UICONTROL Schemas]** van de linkernavigatie en selecteer dan **[!UICONTROL Browse]** , die een overzicht geeft van de beschikbare schema&#39;s. Selecteer vervolgens de ellips (`...`) naast het geselecteerde schema en in een vervolgkeuzelijst worden besturingselementen weergegeven. Selecteren **[!UICONTROL Add to package]** in de vervolgkeuzelijst.

![Lijst met schema&#39;s die het vervolgkeuzemenu weergeven en die de [!UICONTROL Add to package] controle.](../images/ui/sandbox-tooling/add-to-package.png)

Van de **[!UICONTROL Add to package]** selecteert u de **[!UICONTROL Create new package]** -optie. Geef een [!UICONTROL Name] voor uw pakket en een optionele [!UICONTROL Description]selecteert u vervolgens **[!UICONTROL Add]**.

![De [!UICONTROL Add to package] dialoog met [!UICONTROL Create new package] geselecteerd en gemarkeerd [!UICONTROL Add].](../images/ui/sandbox-tooling/create-new-package.png)

U bent teruggekeerd aan **[!UICONTROL Schemas]** milieu. U kunt nu extra objecten toevoegen aan het pakket dat u hebt gemaakt door de volgende stappen hieronder uit te voeren.

### Een object toevoegen aan een bestaand pakket en publiceren {#add-object-to-existing-package}

Als u een lijst met beschikbare schema&#39;s wilt weergeven, selecteert u **[!UICONTROL Schemas]** van de linkernavigatie en selecteer dan **[!UICONTROL Browse]** tab. Selecteer vervolgens de ellips (`...`) naast het geselecteerde schema om besturingsopties in een vervolgkeuzemenu weer te geven. Selecteren **[!UICONTROL Add to package]** in de vervolgkeuzelijst.

![Lijst met schema&#39;s die het vervolgkeuzemenu weergeven en die de [!UICONTROL Add to package] controle.](../images/ui/sandbox-tooling/add-to-package.png)

De **[!UICONTROL Add to package]** wordt weergegeven. Selecteer de **[!UICONTROL Existing package]** en selecteert u vervolgens de optie **[!UICONTROL Package name]** en selecteer het vereiste pakket. Tot slot selecteert u **[!UICONTROL Add]** om je keuzes te bevestigen.

![[!UICONTROL Add to package] een geselecteerd pakket in de vervolgkeuzelijst wordt weergegeven.](../images/ui/sandbox-tooling/add-to-existing-package.png)

De lijst met objecten die aan het pakket zijn toegevoegd, wordt weergegeven. Selecteer **[!UICONTROL Publish]**.

![Een lijst met objecten in het pakket, waarbij de [!UICONTROL Publish] -optie.](../images/ui/sandbox-tooling/publish-package.png)

Selecteren **[!UICONTROL Publish]** de bekendmaking van het pakket te bevestigen.

![Dialoogvenster voor bevestiging van pakket publiceren, met de markering [!UICONTROL Publish] -optie.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Nadat het pakket is gepubliceerd, kan de inhoud ervan niet meer worden gewijzigd. Om compatibiliteitsproblemen te voorkomen, moet u ervoor zorgen dat alle benodigde middelen zijn geselecteerd. Als er wijzigingen moeten worden aangebracht, moet u een nieuw pakket maken.

U bent teruggekeerd aan **[!UICONTROL Packages]** in de [!UICONTROL Sandboxes] omgeving, waar u het nieuwe gepubliceerde pakket kunt zien.

![Lijst met sandboxpakketten die het nieuwe gepubliceerde pakket markeren.](../images/ui/sandbox-tooling/published-packages.png)

## Een pakket importeren naar een doelsandbox {#import-package-to-target-sandbox}

>[!NOTE]
>
>Alle importacties worden vastgelegd in de auditlogboeken.

Navigeer naar de sandboxen om het pakket te importeren in een doelsandbox **[!UICONTROL Browse]** en selecteert u de plusoptie (+) naast de naam van de sandbox.

![De sandboxen **[!UICONTROL Browse]** tabblad de selectie van het importpakket markeren.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Selecteer in het vervolgkeuzemenu de optie **[!UICONTROL Package name]** u wilt importeren in de doelsandbox. Een optioneel object toevoegen **[!UICONTROL Job name]**, die voor toekomstig toezicht zal worden gebruikt, dan selecteren **[!UICONTROL Next]**.

![De pagina met importgegevens die de [!UICONTROL Package name] vervolgkeuzelijst](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

De [!UICONTROL Package object and dependencies] Deze pagina bevat een lijst met alle elementen die in dit pakket zijn opgenomen. Het systeem detecteert automatisch afhankelijke objecten die nodig zijn om geselecteerde bovenliggende objecten te kunnen importeren.

![De [!UICONTROL Package object and dependencies] op de pagina wordt een lijst met elementen weergegeven die in het pakket zijn opgenomen.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>Afhankelijke objecten kunnen worden vervangen door bestaande objecten in de doelsandbox, zodat u bestaande objecten opnieuw kunt gebruiken in plaats van een nieuwe versie te maken. Wanneer u bijvoorbeeld een pakket met schema&#39;s importeert, kunt u de bestaande aangepaste veldgroep en naamruimten in de doelsandbox opnieuw gebruiken. U kunt ook bestaande segmenten in de doelsandbox opnieuw gebruiken wanneer u een pakket importeert, inclusief de stappen voor reizen.

Als u een bestaand object wilt gebruiken, selecteert u het potloodpictogram naast het afhankelijke object. De opties voor het maken van nieuwe of het gebruik van bestaande bestanden worden weergegeven. Selecteer **[!UICONTROL Use existing]**.

![De [!UICONTROL Package object and dependencies] pagina met opties voor afhankelijke objecten [!UICONTROL Create new] en [!UICONTROL Use existing].](../images/ui/sandbox-tooling/use-existing-object.png)

De **[!UICONTROL Field group]** wordt een lijst met veldgroepen weergegeven die beschikbaar zijn voor het object. Selecteer de gewenste veldgroepen en selecteer **[!UICONTROL Save]**.

![Een lijst met velden die worden weergegeven in het dialoogvenster [!UICONTROL Field group] dialoogvenster, markeren [!UICONTROL Save] selectie. ](../images/ui/sandbox-tooling/field-group-list.png)

U bent teruggekeerd aan [!UICONTROL Package object and dependencies] pagina. Van hier, selecteer **[!UICONTROL Finish]** om de pakketimport te voltooien.

![De [!UICONTROL Package object and dependencies] op de pagina wordt een lijst met elementen weergegeven die in het pakket zijn opgenomen. Deze lijst wordt gemarkeerd [!UICONTROL Finish].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

<!--
## Export and import an entire sandbox 

>[!NOTE]
>
>All export and import actions are recorded in the audit logs.

### Export an entire sandbox {#export-entire-sandbox}

To export an entire sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab and select **[!UICONTROL Create package]**.

![The [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab highlighting [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Select **[!UICONTROL Entire sandbox]** for the Type of package in the [!UICONTROL Create package] dialog. Provide a [!UICONTROL Package name] for your package and select the **[!UICONTROL Sandbox]** from the dropdown. Finally, select **[!UICONTROL Create]** to confirm your entries.

![The [!UICONTROL Create package] dialog showing completed fields and highlighting [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

The package is created successfully, select **[!UICONTROL Publish]** to publish the package.

![List of sandbox packages highlighting the new published package.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

You are returned to the **[!UICONTROL Packages]** tab in the [!UICONTROL Sandboxes] environment, where you can see the new published package.

### Import the entire sandbox package {#import-entire-sandbox-package}

To import the package into a target sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Browse]** tab and select the plus (+) option beside the sandbox name.

![The sandboxes **[!UICONTROL Browse]** tab highlighting the import package selection.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Using the dropdown menu, select the full sandbox using the **[!UICONTROL Package name]** dropdown. Add an optional **[!UICONTROL Job name]**, which will be used for future monitoring, then select **[!UICONTROL Next]**.

![The import details page showing the [!UICONTROL Package name] dropdown selection](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>All objects are created as new from the package when importing an entire sandbox. The objects are not listed in the [!UICONTROL Package object and dependencies] page, as there can be multiples. An inline message is displayed, advising of object types that are not supported.

You are taken to the [!UICONTROL Package object and dependencies] page where you can see the number of objects and dependencies that are imported and excluded objects. From here, select **[!UICONTROL Import]** to complete the package import.

 ![The [!UICONTROL Package object and dependencies] page shows the inline message of object types not supported, highlighting [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)
-->

## Importtaken controleren en importobjecten weergeven

Als u de geïmporteerde objecten en de geïmporteerde details wilt bekijken, navigeert u naar de [!UICONTROL Sandboxes] **[!UICONTROL Imports]** en selecteert u het pakket in de lijst. U kunt ook de zoekbalk gebruiken om naar het pakket te zoeken.

![De sandboxen [!UICONTROL Imports] markeert de selectie van het importpakket.](../images/ui/sandbox-tooling/imports-tab.png)

### Geïmporteerde objecten weergeven {#view-imported-objects}

Op de **[!UICONTROL Imports]** in de [!UICONTROL Sandboxes] omgeving, selecteren **[!UICONTROL View imported objects]** in het rechterdetailvenster.

Selecteren **[!UICONTROL View imported objects]** in het rechtervenster met details op het tabblad **[!UICONTROL Imports]** in de [!UICONTROL Sandboxes] milieu.

![De sandboxen [!UICONTROL Imports] tab markeert de [!UICONTROL View imported objects] in het rechterdeelvenster.](../images/ui/sandbox-tooling/view-imported-objects.png)

Gebruik de pijlen om objecten uit te vouwen om de volledige lijst met velden weer te geven die in het pakket zijn geïmporteerd.

![De sandboxen [!UICONTROL Imported objects] een lijst weergeven met objecten die in het pakket zijn geïmporteerd.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### Importdetails weergeven {#view-import-details}

Selecteren **[!UICONTROL View import details]** in het rechtervenster met details in het dialoogvenster **[!UICONTROL Imports]** in de Sandboxomgeving.

![De sandboxen [!UICONTROL Imports] tab markeert de [!UICONTROL View import details] in het rechterdeelvenster.](../images/ui/sandbox-tooling/view-import-details.png)

De **[!UICONTROL Import details]** een gedetailleerde uitsplitsing van de invoer .

![De [!UICONTROL Import details] dialoog met een gedetailleerde uitsplitsing van de invoer.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>Wanneer het importeren is voltooid, ontvangt u meldingen in de gebruikersinterface van het platform. U kunt deze meldingen openen via het waarschuwingspictogram. U kunt hier naar probleemoplossing navigeren als een taak mislukt.

## Volgende stappen

In dit document wordt getoond hoe u de functie voor het gereedmaken van de sandbox in de gebruikersinterface van het Experience Platform kunt gebruiken. Voor informatie over sandboxen raadpleegt u de [gebruikershandleiding sandbox](../ui/user-guide.md).

Voor stappen voor het uitvoeren van verschillende bewerkingen met de sandbox-API raadpleegt u de [sandboxontwikkelaarshandleiding](../api/getting-started.md). Voor een overzicht op hoog niveau van sandboxen in Experience Platform raadpleegt u de [overzichtsdocumentatie](../home.md).
