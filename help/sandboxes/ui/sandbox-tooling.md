---
title: Sandboxen
description: U kunt Sandboxconfiguraties naadloos exporteren en importeren tussen sandboxen.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1449'
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

U kunt de functie voor gereedschappen in de sandbox gebruiken om verschillende objecten te selecteren en deze te exporteren naar een pakket. Een pakket kan bestaan uit één object, meerdere objecten of een hele sandbox. Alle objecten die in een pakket zijn opgenomen, moeten afkomstig zijn uit dezelfde sandbox.

## Objecten ondersteund voor gereedmaken van sandbox {#supported-objects}

De onderstaande tabel bevat een lijst met objecten die momenteel worden ondersteund voor gereedschappen in sandboxen:

| Platform | Object |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | Journeys |
| Klantgegevensplatform | Bronnen |
| Klantgegevensplatform | Segmenten |
| Klantgegevensplatform | Identiteiten |
| Klantgegevensplatform | Beleid |
| Klantgegevensplatform | Schema&#39;s |
| Klantgegevensplatform | Gegevenssets |

De volgende objecten worden geïmporteerd, maar bevinden zich in concept of zijn uitgeschakeld:

| Functie | Object | Status |
| --- | --- | --- |
| Importstatus | Brongegevensstroom | Concept |
| Importstatus | Reis | Concept |
| Verenigd profiel | Schema | Uitgeschakeld |
| Verenigd profiel | Gegevensset | Uitgeschakeld |
| Beleid | Toestemmingsbeleid | Uitgeschakeld |
| Beleid | Beleid inzake gegevensbeheer | Uitgeschakeld |

De onderstaande randgevallen worden niet in het pakket opgenomen:

* Schema-relaties

## Objecten exporteren naar een pakket {#export-objects}

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

## Een volledige sandbox exporteren en importeren

### Een volledige sandbox exporteren {#export-entire-sandbox}

Navigeer naar de [!UICONTROL Sandboxes] **[!UICONTROL Packages]** en selecteert u **[!UICONTROL Create package]**.

![De [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tabmarkering [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Selecteren **[!UICONTROL Entire sandbox]** voor het type pakket in de [!UICONTROL Create package] in. Geef een [!UICONTROL Package name] voor uw pakket en selecteer **[!UICONTROL Sandbox]** in de vervolgkeuzelijst. Tot slot selecteert u **[!UICONTROL Create]** om je inzendingen te bevestigen.

![De [!UICONTROL Create package] dialoogvenster met voltooide velden en markering [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

Het pakket is gemaakt en selecteer **[!UICONTROL Publish]** het pakket publiceren.

![Lijst met sandboxpakketten die het nieuwe gepubliceerde pakket markeren.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

U bent teruggekeerd aan **[!UICONTROL Packages]** in de [!UICONTROL Sandboxes] omgeving, waar u het nieuwe gepubliceerde pakket kunt zien.

### Het volledige sandboxpakket importeren {#import-entire-sandbox-package}

Als u het pakket in een doelsandbox wilt importeren, navigeert u naar de [!UICONTROL Sandboxes] **[!UICONTROL Browse]** en selecteert u de plusoptie (+) naast de naam van de sandbox.

![De sandboxen **[!UICONTROL Browse]** tabblad de selectie van het importpakket markeren.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Selecteer met het vervolgkeuzemenu de volledige sandbox in het dialoogvenster **[!UICONTROL Package name]** vervolgkeuzelijst. Een optioneel object toevoegen **[!UICONTROL Job name]**, die voor toekomstig toezicht zal worden gebruikt, dan selecteren **[!UICONTROL Next]**.

![De pagina met importgegevens die de [!UICONTROL Package name] vervolgkeuzelijst](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Alle objecten worden als nieuw van het pakket gemaakt wanneer een volledige sandbox wordt geïmporteerd. De objecten worden niet vermeld in de [!UICONTROL Package object and dependencies] pagina, aangezien er veelvouden kunnen zijn. Er wordt een inline-bericht weergegeven waarin u wordt gewaarschuwd voor objecttypen die niet worden ondersteund.

U wordt naar de [!UICONTROL Package object and dependencies] pagina waarop u het aantal objecten en afhankelijkheden kunt zien die zijn geïmporteerd en uitgesloten. Van hier, selecteer **[!UICONTROL Import]** om de pakketimport te voltooien.

![De [!UICONTROL Package object and dependencies] op de pagina wordt het inline bericht weergegeven van objecttypen die niet worden ondersteund, markeren [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

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
