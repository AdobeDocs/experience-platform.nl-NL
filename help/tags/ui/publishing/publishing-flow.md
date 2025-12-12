---
title: Publishing Flow
description: Leer meer over het maken van bibliotheken, het testen van builds en het goedkeuren van deze voor productie in Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---

# Publicatiestroom {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="Publicatiestroom"
>abstract="Begrijp de niveaus van gebruikerstoestemmingen die voor de het publiceren stroom worden vereist, met inbegrip van Ontwikkelen, goedkeuren, en publicatierechten."

De publicatiestroom voor tags in Adobe Experience Platform verwijst naar het proces van het maken van bibliotheken, het testen van builds en het goedkeuren van deze voor productie.

Welke acties beschikbaar zijn in een bibliotheek, is afhankelijk van de status van de bibliotheek en het machtigingsniveau. Bovendien beïnvloedt de staat van een bibliotheek ook de middelen het bevat (regels, gegevenselementen, en uitbreidingen) afhankelijk van wat upstream in de het publiceren stroom is.

In de onderstaande secties vindt u informatie over machtigingen, de bibliotheekstatus en de upstream die betrekking heeft op de publicatiestroom.

## Machtigingen {#permissions}

Er zijn verschillende niveaus van gebruikersmachtigingen die belangrijk zijn voor de publicatiestroom. Het gaat hierbij met name om de rechten van de eigenschappen [!UICONTROL Develop] , [!UICONTROL Approve] en [!UICONTROL Publish] :

* **[!UICONTROL Develop]**: biedt de mogelijkheid om bibliotheken te maken, te ontwikkelen en ter goedkeuring in te dienen.
* **[!UICONTROL Approve]**: biedt de mogelijkheid om gefaseerde builds te maken en goed te keuren.
* **[!UICONTROL Publish]**: hiermee kunt u een goedgekeurde bibliotheek publiceren.

Deze rechten zijn niet inclusief. Eén persoon kan de workflow van begin tot eind alleen uitvoeren als aan die persoon alle drie rechten binnen een bepaalde eigenschap zijn toegekend.

Zie de [&#x200B; gids van de gebruikerstoestemmingen &#x200B;](../administration/user-permissions.md) voor meer informatie bij het beheren van toestemmingen voor markeringen.

## Status van bibliotheek {#state}

Wanneer het over de het publiceren stroom aankomt, zijn er vier basisstaten dat een bibliotheek kan zijn in:

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

Deze vier staten worden als kolommen weergegeven op het tabblad **[!UICONTROL Publishing Flow]** .

![](./images/approval-workflow/flow-ui.png)

Er moeten specifieke acties worden ondernomen om een bibliotheek tussen deze staten te verplaatsen. In het volgende diagram wordt elke actie beschreven die een bibliotheek tussen frames verplaatst:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

Wanneer nieuwe bibliotheken worden gemaakt, beginnen deze in de status [!UICONTROL Development] . Wijzigingen in een bibliotheek moeten worden aangebracht terwijl de bibliotheek zich in [!UICONTROL Development] bevindt. Wanneer de ontwikkeling en het testen zijn voltooid, kan de bibliotheek ter goedkeuring worden ingediend.

In de volgende tabel worden de beschikbare acties voor een bibliotheek in de status [!UICONTROL Development] weergegeven:

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Edit] | Met het scherm [!UICONTROL Edit Library] kunt u componenten toevoegen aan of verwijderen uit de bibliotheek. |
| [!UICONTROL Build to Development] | Maak een build voor de bibliotheek. De build wordt gecompileerd en geïmplementeerd in de omgeving waaraan de bibliotheek is toegewezen. Deze stap mislukt als de bibliotheek niet aan een omgeving is toegewezen of als de bibliotheek een wijziging bevat die al in de upstream is gedefinieerd. |
| [!UICONTROL Submit for Approval] | Wijs de bibliotheek niet toe vanuit de ontwikkelomgeving en verplaats de bibliotheek naar de kolom [!UICONTROL Submitted] , zodat een gebruiker met goedkeuringsmachtigingen eraan kan werken. Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Submit & Build to Staging] | Dit kan alleen worden uitgevoerd door een gebruiker met zowel de rechten Ontwikkelen als Goedkeuren. Deze actie verwijdert de toewijzing van de bibliotheek uit de ontwikkelomgeving, verplaatst de bibliotheek naar de status [!UICONTROL Submitted] en bouwt de bibliotheek naar de testomgeving. Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Approve for Publishing] | Dit kan alleen worden uitgevoerd door een gebruiker met zowel de rechten Ontwikkelen als Goedkeuren. Deze actie verwijdert de toewijzing van de bibliotheek uit de ontwikkelomgeving en verplaatst deze naar de status [!UICONTROL Approved] (de testomgeving en de status [!UICONTROL Submitted] worden volledig overgeslagen). Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Approve & Publish to Production] | Dit kan alleen worden uitgevoerd door een gebruiker met de rechten Ontwikkelen, Goedkeuren en Publiceren. Met deze handeling wordt de toewijzing van de bibliotheek aan de ontwikkelomgeving ongedaan gemaakt, verplaatst naar de status [!UICONTROL Approved] en gepubliceerd naar productie. Nadat de productiebuild is voltooid, wordt de bibliotheek naar de status [!UICONTROL Published] verplaatst. Deze optie is alleen ingeschakeld als de meest recente build voor de bibliotheek is gelukt. |
| [!UICONTROL Delete] | Verwijder de bibliotheek van het systeem. Hierdoor wordt de build niet uit de omgeving verwijderd. |

### [!UICONTROL Submitted] {#submitted}

Wanneer een bibliotheek de status [!UICONTROL Submitted] heeft, kan een gebruiker met goedkeuringsmachtigingen de bibliotheek testen in de testomgeving. Wanneer het testen is voltooid, kan de bibliotheek worden goedgekeurd of geweigerd. Geweigerde builds gaan terug naar [!UICONTROL Development] , zodat er aanvullende wijzigingen kunnen worden aangebracht voordat de publicatiestroom opnieuw wordt gestart.

In de volgende tabel worden de beschikbare acties voor een bibliotheek in de status [!UICONTROL Submitted] weergegeven:

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Open] | De inhoud van de bibliotheek weergeven. Wijzigingen zijn niet toegestaan voor bibliotheken buiten de kolom [!UICONTROL Development] . Als er wijzigingen nodig zijn, moet de bibliotheek worden afgewezen zodat er wijzigingen kunnen worden aangebracht in [!UICONTROL Development] . |
| [!UICONTROL Build for Staging] | Bouw de bibliotheek in het opvoeren milieu voor plaatsing. |
| [!UICONTROL Approve for Publishing] | Verplaats de bibliotheek naar de kolom [!UICONTROL Approved] zodat een gebruiker met publicatiemachtigingen eraan kan werken. |
| [!UICONTROL Approve & Publish to Production] | Dit kan alleen worden uitgevoerd door een gebruiker met zowel Goedkeuren als Publicatierechten. Met deze handeling wordt de toewijzing van de bibliotheek aan de testomgeving ongedaan gemaakt, verplaatst naar de status [!UICONTROL Approved] en gepubliceerd naar productie. Nadat de productiebuild is voltooid, wordt de bibliotheek naar de status [!UICONTROL Published] verplaatst. Dit kan met ons zonder een succesvolle bouwstijl in het opvoeren van milieu worden uitgevoerd. |
| [!UICONTROL Reject] | Wijs de bibliotheek niet toe vanuit de testomgeving en verplaats de bibliotheek terug naar de kolom [!UICONTROL Development] voor verdere wijzigingen. |

### [!UICONTROL Approved] {#approved}

Nadat een bibliotheek is goedgekeurd, kan een gebruiker met publicatiemachtigingen de bibliotheek publiceren of afwijzen. Geweigerde builds gaan terug naar [!UICONTROL Development] , zodat verdere wijzigingen kunnen worden aangebracht voordat de publicatiestroom opnieuw begint.

In de volgende tabel worden de beschikbare acties voor een bibliotheek in de status [!UICONTROL Approved] weergegeven:

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Open] | De inhoud van de bibliotheek weergeven. Wijzigingen zijn niet toegestaan voor bibliotheken buiten de kolom [!UICONTROL Development] . Als er wijzigingen nodig zijn, moet de bibliotheek worden afgewezen zodat er wijzigingen kunnen worden aangebracht in [!UICONTROL Development] . |
| [!UICONTROL Build and Publish to Production] | Wijs de bibliotheek uit de testomgeving weg, wijs de bibliotheek aan het productiemilieu toe, en stel het op.<br><br>**Belangrijk**: Wanneer deze optie wordt geselecteerd, wordt uw bibliotheek levend in uw productiemilieu. Controleer of de bibliotheek de gewenste wijzigingen bevat voordat u deze optie selecteert. |
| [!UICONTROL Reject] | Wijs de bibliotheek niet toe vanuit de testomgeving en verplaats de bibliotheek naar de kolom [!UICONTROL Development] voor verdere wijzigingen. |

### [!UICONTROL Published] {#published}

In de kolom [!UICONTROL Published] ziet u welke bibliotheken zijn gepubliceerd en de publicatiedatums. De momenteel gepubliceerde bibliotheek wordt weergegeven met een groene stip ernaast. Tenzij u opnieuw publiceert op een vorige bibliotheek, zal dit altijd de bibliotheek bij de bovenkant van de kolom zijn.

| Actie | Beschrijving |
| --- | --- |
| [!UICONTROL Open] | De inhoud van de bibliotheek weergeven. Wijzigingen zijn niet toegestaan voor bibliotheken buiten de kolom [!UICONTROL Development] . Als u wilt wijzigen wat zich in uw productieomgeving bevindt, moet u een nieuwe bibliotheek maken en deze door het volledige publicatieproces verplaatsen. |
| [!UICONTROL Republish] | Deze actie is alleen beschikbaar voor de vijf laatst gepubliceerde bibliotheken en alleen als de productieomgeving (A) is geconfigureerd met de optie Archiveren uitgeschakeld en (b) een [!UICONTROL Managed by Adobe] host gebruikt op het moment van de build. |
| [!UICONTROL Download] | Deze actie is alleen beschikbaar voor de vijf laatst gepubliceerde bibliotheken en alleen als de productieomgeving (A) is geconfigureerd met de optie Archiveren ingeschakeld en (b) een [!UICONTROL Managed by Adobe] host gebruikt op het moment van de build. |

## Upstream {#upstream}

Nadat u de eerste bibliotheek hebt gepubliceerd, wordt het belangrijk om de rol van de upstream te begrijpen wanneer u nieuwere bibliotheken door de publicatiestroom verplaatst.

Als een bibliotheek zich momenteel in het werkgebied [!UICONTROL Development] , [!UICONTROL Submitted] of [!UICONTROL Approved] bevindt, overerft die bibliotheek de regels, gegevenselementen en extensies van bibliotheken die upstream zijn. Deze geërfte bronnen vormen een &quot;basislijn&quot; voor elke bibliotheek terwijl deze door de publicatiestroom worden verplaatst. In wezen, kunt u aan elke nieuwe bibliotheek eenvoudig als reeks veranderingen in de basislijn denken die door upstream wordt gevestigd. Dit zorgt ervoor dat niets onverwacht van een vorige bibliotheek wordt beschreven wanneer een nieuwe herhaling wordt gepubliceerd.

Wat in de upstream wordt opgenomen, is afhankelijk van het huidige werkgebied van de bibliotheek. Bibliotheken in de kolom [!UICONTROL Approved] nemen bijvoorbeeld alleen bronnen over van de [!UICONTROL Published] -bibliotheek, terwijl bibliotheken onder [!UICONTROL Development] bronnen van alle andere kolommen overnemen.

![](./images/approval-workflow/upstream.png)

Wanneer u een bibliotheek bewerkt in de gebruikersinterface, worden alle bronnen die van de upstream worden overgeërfd, weergegeven in de sectie **[!UICONTROL Resources Upstream]** . Als u deze bronnen wilt weergeven, selecteert u het tabblad Uitvouwen onder de sectiekop.

![](./images/approval-workflow/upstream-collapse.png)

De sectie breidt zich uit om de individuele middelen te tonen die van upstream worden geërft. U kunt de linkerspoorlijn gebruiken om tussen [!UICONTROL Rules], [!UICONTROL Data Elements], en [!UICONTROL Extensions] te filtreren, of de onderzoeksbar te gebruiken om een specifieke middel op naam op te zoeken.

![](./images/approval-workflow/upstream-resources.png)

## Volgende stappen

Deze handleiding biedt een uitgebreid overzicht van de publicatiestroom voor bibliotheken in Adobe Experience Platform. Meer over leren hoe te om uw bibliotheken te publiceren, verwijs naar het [&#x200B; het publiceren overzicht &#x200B;](./overview.md).
