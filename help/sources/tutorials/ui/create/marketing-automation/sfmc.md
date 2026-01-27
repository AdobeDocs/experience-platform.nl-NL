---
title: Sluit uw Salesforce Marketing Cloud (V2)-account aan op Experience Platform via de gebruikersinterface
description: Leer hoe u uw Salesforce Marketing Cloud (V2)-account via de gebruikersinterface kunt verbinden met Experience Platform.
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Verbinden [!DNL Salesforce Marketing Cloud] met Experience Platform

Lees deze handleiding voor informatie over hoe u uw [!DNL Salesforce Marketing Cloud] -account kunt verbinden met Adobe Experience Platform via de werkruimte Bronnen in de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereiste referenties verzamelen

Lees het [[!DNL Salesforce Marketing Cloud]  overzicht &#x200B;](../../../../connectors/marketing-automation/sfmc.md#prerequisites) voor informatie over authentificatie.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Salesforce Marketing Cloud] , gaat u naar de categorie *[!UICONTROL Marketing Automation]* , selecteert u de **[!UICONTROL (V2) Salesforce Marketing Cloud]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![&#x200B; de broncatalogus met de geselecteerde bron van Salesforce Marketing Cloud.](../../../../images/tutorials/create/sfmc/catalog.png)

## Een bestaande account gebruiken {#existing}

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL Salesforce Marketing Cloud] -account die u wilt gebruiken.

![&#x200B; De bestaande rekeningsinterface van het bronwerkschema &#x200B;](../../../../images/tutorials/create/sfmc/existing.png)

## Een nieuwe account maken {#new}

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en beschrijving op onder [!UICONTROL Source connection details] . Daarna, onder [!UICONTROL Account authentication], verstrek waarden voor uw **identiteitskaart van de Cliënt**, **geheim van de Cliënt**, en **het eindpunt van de Basis**. U kunt de [&#x200B; authentificatiegids &#x200B;](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials) voor meer informatie over deze geloofsbrieven lezen. Selecteer **[!UICONTROL Connect to source]** als u klaar bent en wacht een paar seconden totdat de verbinding tot stand is gebracht.

![&#x200B; de nieuwe rekeningsinterface van het bronwerkschema.](../../../../images/tutorials/create/sfmc/new.png)

## Gegevens selecteren

De [!DNL Salesforce Marketing Cloud] -bron ondersteunt alleen gegevensinvoer van [!DNL Salesforce Marketing Cloud] -gegevensextensies.

Gebruik de interface [!UICONTROL Select data] om de gegevensextensie te selecteren die u wilt toevoegen vanuit de instantie [!DNL Salesforce Marketing Cloud] . Zodra u de gegevensuitbreiding selecteert, kunt u het voorproefpaneel gebruiken om te bevestigen dat de dataset de verwachte gebieden bevat alvorens te werk te gaan.

![&#x200B; de uitgezochte gegevensstap van het bronwerkschema &#x200B;](../../../../images/tutorials/create/sfmc/select-data.png)

## Gegevens over gegevensset en gegevensstroom

Daarna, moet u informatie over uw dataset en dataflow verstrekken. Tijdens deze stap, kunt u of een bestaande dataset gebruiken of een nieuwe dataset creëren. Bovendien, kunt u naar keuze uw dataset voor opname aan het Profiel van de Klant in real time tijdens deze stap toelaten.

![&#x200B; de dataset en dataflow detailsstap van het bronwerkschema.](../../../../images/tutorials/create/sfmc/dataset-details.png)

## Toewijzing

In [!DNL Salesforce Marketing Cloud] worden gegevensextensies niet beschouwd als standaardobjecten. Er zijn daarom geen vooraf gedefinieerde of vaste toewijzingsvelden voor een Experience Platform-schema. Terwijl Data Prep in Experience Platform de best-inspanningsgroepering tussen brongebieden van [!DNL Salesforce Marketing Cloud] en het schema van het Model van de Gegevens van de Doelervaring (XDM) uitvoert, kunnen er nog enkele gevallen zijn waar een handrevisie of een aanpassing wordt vereist om unmapped of onjuiste gebieden op te lossen.

![&#x200B; de afbeeldingsstap van het bronwerkschema.](../../../../images/tutorials/create/sfmc/mapping.png)

## Een gegevensstroom plannen

Met uw afbeelding volledig, kunt u een innameprogramma voor uw gegevensstroom nu vormen. Stel de [!UICONTROL Frequency] in op `Once` om een eenmalige invoeruitvoering te configureren. Voor incrementele invoer kunt u de [!UICONTROL Frequency] instellen op `Hour` , `Day` of `Week` . Wanneer u incrementele inname gebruikt, moet u de [!UICONTROL Interval] ook zodanig configureren dat deze de hoeveelheid tijd definieert die tussen inname-bewerkingen plaatsvindt. Als de innamefrequentie bijvoorbeeld is ingesteld op `Day` en als het interval is ingesteld op `15` , worden gegevens elke 15 dagen opgenomen.

>[!TIP]
>
> De innamefrequentie per minuut is niet beschikbaar voor de [!DNL Salesforce Marketing Cloud] bron. Het meest voorkomende schema dat u kunt kiezen, is per uur. Selecteer een schema dat aansluit bij uw behoeften aan gegevensversheid. Houd er rekening mee dat als u een frequentere planning kiest, de kosten van uw computer stijgen.

U moet een delta (datum/tijd) gebied in uw dataset selecteren om stijgende synchronisatie toe te laten. Als uw dataset geen geschikt deltagebied bevat, zult u niet dataflow kunnen tot stand brengen.

![&#x200B; de het plannen stap van het bronwerkschema.](../../../../images/tutorials/create/sfmc/schedule.png)

## Controleren

Met het gevormde ingenschema, gebruik de [!UICONTROL Review] interface om de details van uw gegevensstroom te bevestigen. Selecteer **[!UICONTROL Finish]** om de installatie te voltooien en de gegevensstroom enkele ogenblikken te laten starten.

![&#x200B; de overzichtsstap van het bronwerkschema.](../../../../images/tutorials/create/sfmc/review.png)

## Monitor

Als de gegevensstroom is geselecteerd, worden de gegevens eenmalig teruggevuld en wordt de gegevens vervolgens stapsgewijs gesynchroniseerd volgens het opgegeven schema. De status van synchronisatie kan worden gecontroleerd door aan dataflow te navigeren. Voor meer informatie, leest de gids op [&#x200B; controlemodellen dataflows in UI &#x200B;](../../../../../dataflows/ui/monitor-sources.md).

## Volgende stappen

Deze zelfstudie begeleidde u door uw [!DNL Salesforce Marketing Cloud] (V2) account via de gebruikersinterface aan te sluiten op Experience Platform. U leerde hoe te om een bronrekening te selecteren of te creëren, de vereiste geloofsbrieven te verstrekken, gegevensuitbreidingen te kiezen om in te voeren, dataset en dataflow details te specificeren, uw gegevens in kaart te brengen, opstelling een programma voor gegevensopname, en uw gegevensstromen te controleren. Door deze stappen uit te voeren, hebt u uw [!DNL Salesforce Marketing Cloud] -gegevens met Experience Platform geïntegreerd voor activering en analyse.

Raadpleeg de volgende documentatie voor aanvullende informatie:

* [Overzicht van bronnen](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

