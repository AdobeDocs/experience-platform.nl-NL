---
solution: Experience Platform
title: Overzicht van gegevensbewustzijn in Use Case Playbooks
description: Leer hoe u tijd sneller kunt waarderen door de elementen te kopiëren die in de uiteindelijke inspirerende sandbox zijn gegenereerd naar andere sandboxen.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Door Publish gegenereerde afspeelboeken naar andere sandboxen {#publish-to-other-sandboxes}

Afspeelboeken met hoofdletters/kleine letters zijn marketingsjablonen die zijn ontworpen om elementen te genereren, zoals publiek, schema&#39;s of ritten voor veelvoorkomende gevallen van marketinggebruik. U kunt de elementen die door afspeelboeken zijn gemaakt, testen in de inspirerende sandbox en als u klaar bent, kunt u de elementen importeren in andere ontwikkelingssandboxen voor verdere tests met de gegevens die beschikbaar zijn in die sandboxen. Als u tevreden bent met het testen, kunt u de elementen van ontwikkelingssandboxen verplaatsen naar productiesandboxen.

In bepaalde gevallen hebt u echter al uw eigen schema&#39;s, velden en veldgroepen ingesteld in andere ontwikkelingssandboxen. Hierdoor kunnen sommige elementen die worden gegenereerd door de gebruikscasesjablonen, zoals ritten, niet compatibel zijn met uw gegevens. Lees deze zelfstudie om te begrijpen hoe u de functionaliteit voor gegevensbewustzijn kunt gebruiken om de gegenereerde elementen beter uit te lijnen en aan te vullen met uw bestaande elementen.

## Vereisten {#prerequisites}

Alvorens dit leerprogramma te lezen, doorblader de [&#x200B; beschikbare malplaatjes van het gebruiksgeval playbook &#x200B;](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) en [&#x200B; creeer een geval &#x200B;](/help/use-case-playbooks/playbooks/create-share-reuse.md) van aangewezen playbook.

Wanneer u een instantie maakt, genereert u een set elementen, zoals ritten, segmenten, schema&#39;s en berichten in de inspirerende sandbox. Lees verder voor meer informatie over het kopiëren van deze elementen naar andere sandboxen.

### Een pakket maken en publiceren {#create-publish-package}

>[!NOTE]
>
> U kunt pakketten alleen importeren in andere ontwikkelingssandboxen. Wanneer u alle benodigde wijzigingen of updates hebt aangebracht, kunt u de elementen of pakketten uit deze ontwikkelingssandboxen in productie importeren. U kunt niet rechtstreeks van de zandbakken van de Playbooks van het Gebruik aan productie invoeren.

1. Als u objecten van de inspirerende sandbox wilt importeren in een andere sandbox, bladert u naar een gewenste instantie van een afspeelboek met een gebruiksscenario en selecteert u **[!UICONTROL Publish to a different sandbox]** om de artefacten als een pakket te exporteren.

   ![&#x200B; GIF die de verschillende instanties van het gebruiksgeval tonen &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Nadat u de knop **[!UICONTROL Publish to a different sandbox]** hebt geselecteerd, wordt een modaal item weergegeven. Vul de naam en de optionele beschrijving in en selecteer **[!UICONTROL Create]** . Deze stap bundelt de gegenereerde elementen in een pakket dat kan worden geïmporteerd in een andere sandbox.

   ![&#x200B; modal A voor het creëren van een pakket &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Navigeer aan de **zandbakken** pagina in de linkerzijnavigatie en selecteer het **lusje van Pakketten**, vind uw pakket, en publiceer het. Om een pakket te publiceren dat in ontwerpstaat is, volg de stappen in het [&#x200B; zandbak tooling &#x200B;](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) document.

   ![&#x200B; Pakket in ontwerp of unpublished staat &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![&#x200B; het Publiceren van het pakket &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Nadat publiceren slaagt, op de pakketdoorbladeren pagina zou u **moeten zien +** knoop die naast de naam wordt toegelaten.

   ![&#x200B; lusje van Pakketten in de pagina Sandboxes &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Het pakket kan niet worden geïmporteerd terwijl het zich nog in de conceptmodus bevindt. Open daarom de detailpagina van het pakket en publiceer het pakket.

5. Selecteer **+** controle en begin het werkschema om de activa in te voeren die door het gebruikscasplaybook in **[!UICONTROL Target sandbox]** worden geproduceerd. Selecteer een doelsandbox en bevestig de pakketnaam die u wilt importeren met de vervolgkeuzelijst. Voeg de taakdetails zoals taaknaam en taakbeschrijving toe voordat u verdergaat met de volgende stap.

   ![&#x200B; begin het invoerwerkschema, uitgezochte doel, bevestig pakket, voeg baandetails toe.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. In de stap **[!UICONTROL View dependencies]** kunt u schema&#39;s toewijzen en andere elementen uit de inspirerende sandbox kopiëren naar de doelsandbox. De knop **[!UICONTROL Finish]** wordt uitgeschakeld totdat u elk schema toewijst.

   ![&#x200B; de schema&#39;s van de Kaart in de &quot;gebiedsdelen van de Mening&quot;stap, toelatend de knoop van de Afwerking.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Kaartschema&#39;s {#map-schemas}

1. Wijs het eerste schema toe. Het dialoogvenster Schema-toewijzing geeft een vervolgkeuzelijst weer om het doelschema te selecteren. Als het bronschema een profielschema is, dan zijn er geen andere opties van het doelschema naast het [&#x200B; individuele schema van het verenigingsprofiel &#x200B;](/help/xdm/classes/individual-profile.md). Wanneer de pagina voor het eerst wordt weergegeven, ziet u automatisch gegenereerde toewijzingsaanbevelingen tussen Source-gegevens en doelvelden. U kunt de toewijzingen bewerken door het doelveld te selecteren en vervolgens een nieuw veld te selecteren. Als u de voorgestelde afbeeldingen wijzigt, gebruik **bevestigen** knoop om de nieuwe afbeeldingen te bevestigen en om het even welke fouten te tonen die met de nieuwe afbeeldingen kunnen worden verbonden. Selecteer **sparen** zodra de afbeelding volledig is.

   ![&#x200B; de toewijzingsdialoog van het Schema met een dropdown om een doelschema te selecteren.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Wijs alle velden in de schema&#39;s verder toe. Als het schema een [&#x200B; gebeurtenisschema &#x200B;](/help/xdm/classes/experienceevent.md) is, toont de dialoog een dropdown waar u alle gebeurtenisschema&#39;s in de doelzandbak kunt bekijken.

   ![&#x200B; selecteer een doelschema van dropdown &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Selecteer een schema van beschikbare schema&#39;s in de **zandbak van het Doel**.

   ![&#x200B; selecteer een schema &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Voltooi de afbeelding en selecteer **sparen**.

   ![&#x200B; sparen afbeelding &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Zodra u afbeelding alle gebieden in de schema&#39;s hebt voltooid, uitgezochte **Afwerking** om het de invoerwerkschema te voltooien.

   ![&#x200B; beëindigt de stroom &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > U kunt geen elementen wijzigen, behalve de schema&#39;s, omdat dit een inspirerende sandbox is, maar wel omdat ze afhankelijk zijn van het pakket.

### Importstatus {#import-status}

1. U wordt automatisch opnieuw gericht aan de [**invoer**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) pagina waar u de vooruitgang van uw invoer kunt zien.

   ![&#x200B; Pagina die invoervooruitgang toont &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Tijdens het importeren van het pakket worden de elementen van het pakket gemaakt in de doelsandbox. Zodra deze bewerking is voltooid, verwijzen ze naar de velden die u tijdens het importeren hebt toegewezen. Het proces is nu voltooid en de elementen van de inspirerende sandbox zijn nu ook aanwezig in de doelsandbox die u kunt testen.

   ![&#x200B; Gegenereerde activa in de doelzandbak &#x200B;](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Volgende stappen

Na het lezen van deze gids, hebt u nu een beter inzicht in hoe te gebruik caseplaybooks samen met [&#x200B; zandbak tooling &#x200B;](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) om uitvoerbare reizen tot stand te brengen die uw schema&#39;s van verwijzingen voorzien. Leer meer over de gemeenschappelijke [&#x200B; het gebruiksgevallen van Real-Time CDP &#x200B;](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
