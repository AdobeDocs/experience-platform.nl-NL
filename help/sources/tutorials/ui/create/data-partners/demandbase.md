---
title: Connect Demandbase Intent to Experience Platform via de gebruikersinterface
description: Leer hoe u demandbase Intent kunt verbinden met Experience Platform
exl-id: 7dc87067-cdf6-4dde-b077-19666dcb12e2
source-git-commit: 04af34d439ba76b0d0053ba9de45ca962458d3e8
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---

# Verbinding maken [!DNL Demandbase Intent] met Experience Platform via de gebruikersinterface

Lees deze handleiding voor informatie over hoe u uw [!DNL Demandbase Intent] -account kunt verbinden met Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Real-Time CDP B2B edition ](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition is speciaal-gebouwd voor marketers die in een zaken-aan-zaken de dienstmodel werken. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.
* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereisten

Lees het [[!DNL Demandbase Intent]  overzicht ](../../../../connectors/data-partners/demandbase.md) voor informatie over hoe te om uw authentificatiegeloofsbrieven terug te winnen.

## Navigeren door de catalogus met bronnen {#navigate}

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . U kunt de juiste categorie selecteren in het deelvenster *[!UICONTROL Categories]* . U kunt ook de zoekbalk gebruiken om naar de specifieke bron te navigeren die u wilt gebruiken.

Als u [!DNL Demandbase] wilt gebruiken, selecteert u de **[!UICONTROL Demandbase Intent]** bronkaart onder [!UICONTROL Data & Identity Partners] en selecteert u vervolgens **[!UICONTROL Add data]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus met de &quot;Vraag geselecteerde Intentie&quot;kaart van de Intentie.](../../../../images/tutorials/create/demandbase/catalog.png)

## Verificatie {#authentication}

### Een bestaande account gebruiken {#existing}

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens de account die u wilt gebruiken in de lijst met accounts in de interface.

Nadat u uw account hebt geselecteerd, selecteert u **[!UICONTROL Next]** om door te gaan naar de volgende stap.

![ de bestaande rekeningsinterface van het bronwerkschema.](../../../../images/tutorials/create/demandbase/existing.png)

### Een nieuwe account maken {#create}

Als u geen bestaand account hebt, moet u een nieuw account maken door de vereiste verificatiereferenties op te geven die overeenkomen met uw bron.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een accountnaam en optioneel een beschrijving voor uw accountgegevens. Geef vervolgens de juiste verificatiewaarden op om uw bron te verifiëren op basis van Experience Platform. U moet over de volgende referenties beschikken om verbinding te maken met uw [!DNL Demandbase Intent] -account:

* **zeer belangrijke identiteitskaart van de Toegang**: Uw [!DNL Demandbase] toegangs belangrijkste identiteitskaart Dit is een alfanumerieke tekenreeks van 61 tekens die vereist is om uw account bij Experience Platform te verifiëren.
* **Geheime toegangstoets**: Uw [!DNL Demandbase] geheime toegangstoets. Dit is een tekenreeks van 40 tekens met een basiscodering van 64 tekens die vereist is om uw account bij Experience Platform te verifiëren.
* **naam van het Emmertje**: Uw [!DNL Demandbase] emmertje waarvan de gegevens zullen worden getrokken.

![ de nieuwe rekeningsinterface van het bronwerkschema.](../../../../images/tutorials/create/demandbase/new.png)

## Gegevens over gegevensstroom opgeven {#provide-dataflow-details}

Nadat uw account is geverifieerd en verbinding heeft gemaakt, moet u nu de volgende gegevens voor uw gegevensstroom opgeven:

* **naam Dataflow**: De naam van uw dataflow. U kunt deze naam gebruiken om naar uw gegevensstroom in UI te zoeken, zodra het is gecreeerd en verwerkt.
* **Beschrijving**: (Facultatief) een korte verklaring of extra informatie voor uw dataflow.
* **bron van het Domein**: Het domein of websitegebied dat uw bronrekeningsverslagen tegen de rekeningen van Experience Platform aanpast. Deze waarde kan afhankelijk zijn van uw configuraties. Indien niet opgegeven, wordt het domein standaard ingesteld op `accountOrganization.website` .

![ de dataflow detailstap van het bronwerkschema.](../../../../images/tutorials/create/demandbase/dataflow-detail.png)

## Dataflow plannen {#schedule-dataflow}

Daarna, gebruik de het plannen interface om een innameprogramma voor uw dataflow te vormen.

* **Frequentie**: Vorm frequentie om erop te wijzen hoe vaak dataflow zou moeten lopen. U kunt uw [!DNL Demandbase] gegevensstroom plannen om gegevens met een wekelijkse snelheid in te voeren.
* **Interval**: Het interval vertegenwoordigt de hoeveelheid tijd tussen elke opnamecyclus. Het enige ondersteunde interval voor een [!DNL Demandbase] dataflow is `1` . Dit betekent dat uw gegevensstroom gegevens eenmaal per week, elke week, zal innemen.
* **tijd van het Begin**: De begintijd dicteert wanneer de eerste looppasherhaling van uw dataflow zal voorkomen. [!DNL Demandbase] laat gegevens eenmaal per week, op maandag, om 12:00 uur UTC naar Adobe gaan. :00 Daarom moet u uw ingangsbegintijd na 12 :00 PM UTC plaatsen. Bovendien moet u de innametijd met [!DNL Demandbase] bevestigen, aangezien deze hun planning kunnen veranderen, wanneer het laten vallen van dossiers aan Adobe.
* **Achtergrond**: De achtergrond bepaalt welke gegevens aanvankelijk worden opgenomen. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als terugvullen is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen.

Selecteer **[!UICONTROL Next]** als u het schema voor inname van de gegevensstroom hebt geconfigureerd.

![ De het plannen interface van het bronwerkschema.](../../../../images/tutorials/create/demandbase/scheduling.png)

## Gegevensstroom controleren {#review-dataflow}

De laatste stap in het proces voor het maken van een gegevensstroom is het controleren van de gegevensstroom voordat deze wordt uitgevoerd. Gebruik de stap *[!UICONTROL Review]* om de details van de nieuwe gegevensstroom te bekijken voordat deze wordt uitgevoerd. De details worden gegroepeerd in de volgende categorieën:

* **Verbinding**: Toont het brontype, de relevante weg van het gekozen brondossier, en het aantal kolommen binnen dat brondossier.
* **Plannend**: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

![ de overzichtsinterface van het bronwerkschema.](../../../../images/tutorials/create/demandbase/review.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt om intentgegevens van uw [!DNL Demandbase] -bron naar Experience Platform te verzenden. Voor extra bronnen raadpleegt u de documentatie die hieronder wordt beschreven.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamesnelheden, succes, en fouten te bekijken. Voor meer informatie over hoe te om dataflow te controleren, bezoek het leerprogramma op [ controlerekeningen en dataflows in UI ](../../../../../dataflows/ui/monitor-sources.md).

### Uw gegevensstroom bijwerken

Om configuraties voor uw dataflows bij te werken die, afbeelding, en algemene informatie plannen, bezoek het leerprogramma op [ bijwerken brondataflows in UI ](../../update-dataflows.md).

### Uw gegevensstroom verwijderen

U kunt gegevensstromen verwijderen die niet meer nodig zijn of die onjuist zijn gemaakt met de functie **[!UICONTROL Delete]** die beschikbaar is in de **[!UICONTROL Dataflows]** -werkruimte. Voor meer informatie over hoe te om dataflows te schrappen, bezoek het leerprogramma bij [ het schrappen van dataflows in UI ](../../delete.md).
