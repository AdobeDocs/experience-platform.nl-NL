---
title: Publishing Flow
description: Leer meer over het maken van bibliotheken, het testen van builds en het goedkeuren van deze voor productie in Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 0%

---

# Publicatiestroom

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De publicatiestroom voor tags in Adobe Experience Platform verwijst naar het proces van het maken van bibliotheken, het testen van builds en het goedkeuren van deze voor productie.

Welke acties beschikbaar zijn in een bibliotheek, is afhankelijk van de status van de bibliotheek en het machtigingsniveau. Bovendien beïnvloedt de staat van een bibliotheek ook de middelen het bevat (regels, gegevenselementen, en uitbreidingen) afhankelijk van wat upstream in de het publiceren stroom is.

In de onderstaande secties vindt u informatie over machtigingen, de bibliotheekstatus en de upstream die betrekking heeft op de publicatiestroom.

## Toestemmingen {#permissions}

Er zijn verschillende niveaus van gebruikerstoestemmingen die voor de het publiceren stroom belangrijk zijn; in het bijzonder [!UICONTROL Develop], [!UICONTROL Approve], en [!UICONTROL Publish] eigendomsrechten:

* **[!UICONTROL Develop]**: Omvat de capaciteit om bibliotheken tot stand te brengen, voor ontwikkeling te bouwen, en voor goedkeuring voor te leggen.
* **[!UICONTROL Approve]**: Omvat de capaciteit om voor het opvoeren te bouwen en gefaseerde bouwstijlen goed te keuren.
* **[!UICONTROL Publish]**: Bevat de mogelijkheid om een goedgekeurde bibliotheek te publiceren.

Deze rechten zijn niet inclusief. Eén persoon kan de workflow van begin tot eind alleen uitvoeren als aan die persoon alle drie rechten binnen een bepaalde eigenschap zijn toegekend.

Zie de [gebruikershandleiding voor machtigingen](../administration/user-permissions.md) voor meer informatie over het beheren van toestemmingen voor markeringen.

## Status van bibliotheek {#state}

Wanneer het over de het publiceren stroom aankomt, zijn er vier basisstaten dat een bibliotheek kan zijn in:

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

Deze vier staten worden als kolommen weergegeven in de **[!UICONTROL Publishing Flow]** tab.

![](./images/approval-workflow/flow-ui.png)

Er moeten specifieke acties worden ondernomen om een bibliotheek tussen deze staten te verplaatsen. In het volgende diagram wordt elke actie beschreven die een bibliotheek tussen frames verplaatst:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

Wanneer nieuwe bibliotheken worden gemaakt, beginnen deze in het dialoogvenster [!UICONTROL Development] status. Alle wijzigingen in een bibliotheek moeten worden aangebracht terwijl de bibliotheek zich in [!UICONTROL Development]. Wanneer de ontwikkeling en het testen zijn voltooid, kan de bibliotheek ter goedkeuring worden ingediend.

In de volgende tabel worden de beschikbare acties voor een bibliotheek in de [!UICONTROL Development] status:

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Edit] | Gebruik de [!UICONTROL Edit Library] scherm om componenten aan de bibliotheek toe te voegen of te verwijderen. |
| [!UICONTROL Build to Development] | Maak een build voor de bibliotheek. De build wordt gecompileerd en geïmplementeerd in de omgeving waaraan de bibliotheek is toegewezen. Deze stap mislukt als de bibliotheek niet aan een omgeving is toegewezen of als de bibliotheek een wijziging bevat die al in de upstream is gedefinieerd. |
| [!UICONTROL Submit for Approval] | Wijs de bibliotheek niet toe aan de ontwikkelomgeving en verplaats de bibliotheek naar de [!UICONTROL Submitted] kolom voor een gebruiker met toestemmingen om aan te werken. Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Submit & Build to Staging] | Dit kan alleen worden uitgevoerd door een gebruiker met zowel de rechten Ontwikkelen als Goedkeuren. Hiermee wordt de toewijzing van de bibliotheek aan de ontwikkelomgeving ongedaan gemaakt, wordt de bibliotheek naar de [!UICONTROL Submitted] status en bouwt de bibliotheek naar de testomgeving. Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Approve for Publishing] | Dit kan alleen worden uitgevoerd door een gebruiker met zowel de rechten Ontwikkelen als Goedkeuren. Met deze handeling wordt de toewijzing van de bibliotheek aan de ontwikkelomgeving ongedaan gemaakt en wordt de bibliotheek naar de [!UICONTROL Approved] staat - de testomgeving en de [!UICONTROL Submitted] staat volledig. Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Approve & Publish to Production] | Dit kan alleen worden uitgevoerd door een gebruiker met de rechten Ontwikkelen, Goedkeuren en Publiceren. Met deze handeling wordt de toewijzing van de bibliotheek aan de ontwikkelomgeving ongedaan gemaakt en wordt de bibliotheek naar de [!UICONTROL Approved] staat en publiceert naar productie. Na voltooiing van de productiebuild wordt de bibliotheek verplaatst naar de [!UICONTROL Published] status. Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Delete] | Verwijder de bibliotheek van het systeem. Hierdoor wordt de build niet uit de omgeving verwijderd. |

### [!UICONTROL Submitted] {#submitted}

Wanneer een bibliotheek zich in de [!UICONTROL Submitted] een gebruiker met goedkeuringsmachtigingen kan de bibliotheek in de testomgeving testen. Wanneer het testen is voltooid, kan de bibliotheek worden goedgekeurd of geweigerd. Geweigerde builds gaan terug naar [!UICONTROL Development] Er kunnen dus aanvullende wijzigingen worden aangebracht voordat u de publicatiestroom opnieuw start.

In de volgende tabel worden de beschikbare acties voor een bibliotheek in de [!UICONTROL Submitted] status:

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Open] | De inhoud van de bibliotheek weergeven. Wijzigingen zijn niet toegestaan voor bibliotheken buiten de [!UICONTROL Development] kolom. Als er wijzigingen nodig zijn, moet de bibliotheek worden afgewezen zodat er wijzigingen kunnen worden aangebracht in [!UICONTROL Development]. |
| [!UICONTROL Build for Staging] | Bouw de bibliotheek in het opvoeren milieu voor plaatsing. |
| [!UICONTROL Approve for Publishing] | De bibliotheek naar de [!UICONTROL Approved] kolom voor een gebruiker met publicatiemachtigingen om aan te werken. |
| [!UICONTROL Approve & Publish to Production] | Dit kan alleen worden uitgevoerd door een gebruiker met zowel Goedkeuren als Publicatierechten. Hiermee wordt de toewijzing van de bibliotheek uit de testomgeving verwijderd en verplaatst naar de [!UICONTROL Approved] staat en publiceert naar productie. Na voltooiing van de productiebuild wordt de bibliotheek verplaatst naar de [!UICONTROL Published] status. Dit kan met ons zonder een succesvolle bouwstijl in het opvoeren van milieu worden uitgevoerd. |
| [!UICONTROL Reject] | Wijs de bibliotheek niet toe vanuit de testomgeving en verplaats de bibliotheek terug naar de [!UICONTROL Development] kolom voor verdere wijzigingen. |

### [!UICONTROL Approved] {#approved}

Nadat een bibliotheek is goedgekeurd, kan een gebruiker met publicatiemachtigingen de bibliotheek publiceren of afwijzen. Geweigerde builds gaan terug naar [!UICONTROL Development] zodat verdere wijzigingen kunnen worden aangebracht voordat de publicatiestroom opnieuw begint.

In de volgende tabel worden de beschikbare acties voor een bibliotheek in de [!UICONTROL Approved] status:

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Open] | De inhoud van de bibliotheek weergeven. Wijzigingen zijn niet toegestaan voor bibliotheken buiten de [!UICONTROL Development] kolom. Als er wijzigingen nodig zijn, moet de bibliotheek worden afgewezen zodat er wijzigingen kunnen worden aangebracht in [!UICONTROL Development]. |
| [!UICONTROL Build and Publish to Production] | Wijs de bibliotheek uit de testomgeving weg, wijs de bibliotheek aan het productiemilieu toe, en stel het op.<br><br>**Belangrijk**: Als deze optie is geselecteerd, wordt uw bibliotheek live in uw productieomgeving. Controleer of de bibliotheek de gewenste wijzigingen bevat voordat u deze optie selecteert. |
| [!UICONTROL Reject] | Wijs de bibliotheek niet toe aan de testomgeving en verplaats de bibliotheek naar de [!UICONTROL Development] kolom voor verdere wijzigingen. |

### [!UICONTROL Published] {#published}

De [!UICONTROL Published] in de kolom wordt aangegeven welke bibliotheken zijn gepubliceerd en welke publicatiedata zijn gepubliceerd. De momenteel gepubliceerde bibliotheek wordt weergegeven met een groene stip ernaast. Tenzij u een republish op een vorige bibliotheek hebt uitgevoerd, zal dit altijd de bibliotheek bij de bovenkant van de kolom zijn.

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Open] | De inhoud van de bibliotheek weergeven. Wijzigingen zijn niet toegestaan voor bibliotheken buiten de [!UICONTROL Development] kolom. Als u wilt wijzigen wat zich in uw productieomgeving bevindt, moet u een nieuwe bibliotheek maken en deze door het volledige publicatieproces verplaatsen. |
| [!UICONTROL Republish] | Deze actie is alleen beschikbaar voor de vijf laatst gepubliceerde bibliotheken en alleen als de productieomgeving (A) is geconfigureerd met de optie Archiveren uitgeschakeld en (b) een [!UICONTROL Managed by Adobe] host op het moment van de build. |
| [!UICONTROL Download] | Deze actie is alleen beschikbaar voor de vijf laatst gepubliceerde bibliotheken en alleen als de productieomgeving (A) is geconfigureerd met de optie Archiveren ingeschakeld en (b) een [!UICONTROL Managed by Adobe] host op het moment van de build. |

## Upstream {#upstream}

Nadat u de eerste bibliotheek hebt gepubliceerd, wordt het belangrijk om de rol van de upstream te begrijpen wanneer u nieuwere bibliotheken door de publicatiestroom verplaatst.

Als er momenteel een bibliotheek in de [!UICONTROL Development], [!UICONTROL Submitted], of [!UICONTROL Approved] in het werkgebied, neemt die bibliotheek de regels, gegevenselementen en extensies over van bibliotheken die upstream zijn. Deze geërfte bronnen vormen een &quot;basislijn&quot; voor elke bibliotheek terwijl deze door de publicatiestroom worden verplaatst. In wezen, kunt u aan elke nieuwe bibliotheek eenvoudig als reeks veranderingen in de basislijn denken die door upstream wordt gevestigd. Dit zorgt ervoor dat niets onverwacht van een vorige bibliotheek wordt beschreven wanneer een nieuwe herhaling wordt gepubliceerd.

Wat in de upstream wordt opgenomen, is afhankelijk van het huidige werkgebied van de bibliotheek. Bibliotheken in het dialoogvenster [!UICONTROL Approved] kolom erft alleen bronnen van de [!UICONTROL Published] bibliotheek, terwijl bibliotheken onder [!UICONTROL Development] erven middelen van alle andere kolommen.

![](./images/approval-workflow/upstream.png)

Wanneer u een bibliotheek in de gebruikersinterface bewerkt, worden alle bronnen die van de upstream zijn overgeërfd, weergegeven in het dialoogvenster **[!UICONTROL Resources Upstream]** sectie. Als u deze bronnen wilt weergeven, selecteert u het tabblad Uitvouwen onder de sectiekop.

![](./images/approval-workflow/upstream-collapse.png)

De sectie breidt zich uit om de individuele middelen te tonen die van upstream worden geërft. U kunt de linkerrail gebruiken om te filteren tussen [!UICONTROL Rules], [!UICONTROL Data Elements], en [!UICONTROL Extensions]of gebruik de zoekbalk om een bepaalde bron op naam op te zoeken.

![](./images/approval-workflow/upstream-resources.png)

## Volgende stappen

Deze handleiding biedt een uitgebreid overzicht van de publicatiestroom voor bibliotheken in Adobe Experience Platform. Raadpleeg voor meer informatie over het publiceren van bibliotheken de [publicatieoverzicht](./overview.md).
