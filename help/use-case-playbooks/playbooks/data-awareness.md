---
solution: Experience Platform
title: Overzicht van gegevensbewustzijn in Use Case Playbooks
description: Leer hoe u tijd sneller kunt waarderen door de elementen te kopiëren die in de uiteindelijke inspirerende sandbox zijn gegenereerd naar andere sandboxen.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: ecce42e2c759bda31bc37d0aae1da2c7b3d141fc
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Door afspeelboeken gegenereerde elementen publiceren naar andere sandboxen {#publish-to-other-sandboxes}

Afspeelboeken met hoofdletters/kleine letters zijn marketingsjablonen die zijn ontworpen om elementen te genereren, zoals publiek, schema&#39;s of ritten voor veelvoorkomende gevallen van marketinggebruik. U kunt de elementen die door afspeelboeken zijn gemaakt, testen in de inspirerende sandbox en als u klaar bent, kunt u de elementen importeren in andere ontwikkelingssandboxen voor verdere tests met de gegevens die beschikbaar zijn in die sandboxen. Als u tevreden bent met het testen, kunt u de elementen van ontwikkelingssandboxen verplaatsen naar productiesandboxen.

In bepaalde gevallen hebt u echter al uw eigen schema&#39;s, velden en veldgroepen ingesteld in andere ontwikkelingssandboxen. Hierdoor kunnen sommige elementen die worden gegenereerd door de gebruikscasesjablonen, zoals ritten, niet compatibel zijn met uw gegevens. Lees deze zelfstudie om te begrijpen hoe u de functionaliteit voor gegevensbewustzijn kunt gebruiken om de gegenereerde elementen beter uit te lijnen en aan te vullen met uw bestaande elementen.

## Vereisten {#prerequisites}

Blader voordat u deze zelfstudie leest naar de [beschikbare use case playbook-sjablonen](/help/use-case-playbooks/playbooks/discover.md#search-and-filter) en [een instantie maken](/help/use-case-playbooks/playbooks/create-share-reuse.md) van een voorkeursboek.

Wanneer u een instantie maakt, genereert u een set elementen, zoals ritten, segmenten, schema&#39;s en berichten in de inspirerende sandbox. Lees verder voor meer informatie over het kopiëren van deze elementen naar andere sandboxen.

### Een pakket maken en publiceren {#create-publish-package}

>[!NOTE]
>
> U kunt pakketten alleen importeren in andere ontwikkelingssandboxen. Wanneer u alle benodigde wijzigingen of updates hebt aangebracht, kunt u de elementen of pakketten uit deze ontwikkelingssandboxen in productie importeren. U kunt niet rechtstreeks van de zandbakken van de Playbooks van het Gebruik aan productie invoeren.

1. Als u objecten van de inspirerende sandbox wilt importeren in een andere sandbox, bladert u naar een gewenste instantie van een afspeelboek met een use-case en selecteert u **[!UICONTROL Publish to a different sandbox]** om de artefacten als pakket uit te voeren.

   ![GIF dat de verschillende instanties van het gebruiksgeval toont](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Wanneer u de **[!UICONTROL Publish to a different sandbox]** wordt een modaal weergegeven. Vul de naam en de optionele beschrijving in en selecteer **[!UICONTROL Create]**. Deze stap bundelt de gegenereerde elementen in een pakket dat kan worden geïmporteerd in een andere sandbox.

   ![Een modus voor het maken van een pakket](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Ga naar de **Sandboxen** pagina in de linkerzijnavigatie en selecteer de **Pakketten** , zoekt u het pakket en publiceert u het. Voer de stappen in het dialoogvenster [sandbox, gereedschap](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) document.

   ![Pakket maken in concept of niet-gepubliceerde status](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Het pakket publiceren](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Nadat de publicatie is gelukt, kunt u op de pagina met de pakketten bladeren. **+** ingeschakeld naast de naam.

   ![Het tabblad Pakketten in de pagina Sandboxen](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Het pakket kan niet worden geïmporteerd terwijl het zich nog in de conceptmodus bevindt. Open daarom de detailpagina van het pakket en publiceer het pakket.

5. Selecteer de **+** de workflow beheren en starten om de elementen die worden gegenereerd door de afspeelmap met het gebruiksscenario te importeren in de **[!UICONTROL Target sandbox]**. Selecteer een doelsandbox en bevestig de pakketnaam die u wilt importeren met de vervolgkeuzelijst. Voeg de taakdetails zoals taaknaam en taakbeschrijving toe voordat u verdergaat met de volgende stap.

   ![Start de importworkflow, selecteer doel, bevestig het pakket en voeg taakdetails toe.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. In de **[!UICONTROL View dependencies]** stap, kunt u schema&#39;s in kaart brengen en andere activa van de inspirerende zandbak kopiëren in de doelzandbak. De **[!UICONTROL Finish]** is uitgeschakeld totdat u elk schema toewijst.

   ![De schema&#39;s van de kaart in de &quot;Gedeelten van de Mening&quot;stap, toelatend de knoop van de Afwerking.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Kaartschema&#39;s {#map-schemas}

1. Wijs het eerste schema toe. Het dialoogvenster Schema-toewijzing geeft een vervolgkeuzelijst weer om het doelschema te selecteren. Als het bronschema een profielschema is, dan zijn er geen andere opties van het doelschema naast [individueel vakprofielschema](/help/xdm/classes/individual-profile.md). U kunt automatisch gegenereerde toewijzingsaanbevelingen tussen Brongegevens en Doelvelden zien wanneer de pagina voor het eerst wordt weergegeven. U kunt de toewijzingen bewerken door het doelveld te selecteren en vervolgens een nieuw veld te selecteren. Als u de voorgestelde toewijzingen wijzigt, gebruikt u de opdracht **Valideren** om de nieuwe toewijzingen te valideren en eventuele fouten weer te geven die aan de nieuwe toewijzingen kunnen worden gekoppeld. Selecteren **Opslaan** zodra de toewijzing is voltooid.

   ![Dialoogvenster voor schematoewijzing met een vervolgkeuzelijst om een doelschema te selecteren.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Wijs alle velden in de schema&#39;s verder toe. Als het schema een [gebeurtenisschema](/help/xdm/classes/experienceevent.md)In dit dialoogvenster wordt een vervolgkeuzelijst weergegeven waarin u alle gebeurtenisschema&#39;s in de doelsandbox kunt weergeven.

   ![Doelschema selecteren in vervolgkeuzelijst](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Selecteer een schema van beschikbare schema&#39;s in **Doelsandbox**.

   ![Selecteer een schema](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. De toewijzing voltooien en selecteren **Opslaan**.

   ![Toewijzing opslaan](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Als u alle velden in de schema&#39;s hebt toegewezen, selecteert u **Voltooien** om de importworkflow te voltooien.

   ![De stroom voltooien](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > U kunt geen elementen wijzigen, behalve de schema&#39;s, omdat dit een inspirerende sandbox is, maar wel omdat ze afhankelijk zijn van het pakket.

### Importstatus {#import-status}

1. U wordt automatisch omgeleid naar de [**Invoer**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) pagina waarop u de voortgang van het importeren kunt zien.

   ![Pagina met voortgang bij importeren](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Tijdens het importeren van het pakket worden de elementen van het pakket gemaakt in de doelsandbox. Zodra deze bewerking is voltooid, verwijzen ze naar de velden die u tijdens het importeren hebt toegewezen. Het proces is nu voltooid en de elementen van de inspirerende sandbox zijn nu ook aanwezig in de doelsandbox die u kunt testen.

   ![Gegenereerde elementen in de doelsandbox](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u nu een beter inzicht in hoe u de afspeelboeken van hoofdletters en kleine letters samen met [sandbox, gereedschap](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) om uitvoerbare reizen tot stand te brengen die uw schema&#39;s van verwijzingen voorzien. Meer informatie over de algemene [Real-Time CDP-gebruikskwesties](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
