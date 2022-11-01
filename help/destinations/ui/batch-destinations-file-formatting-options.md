---
description: Leer hoe u opties voor bestandsindeling kunt configureren wanneer u gegevens activeert naar bestandsbestemmingen
title: (Bèta) Vorm dossier het formatteren opties voor op dossier-gebaseerde bestemmingen
source-git-commit: 23a7a1997e05d2bde26de5b73a23ea051bf2b3bb
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# (Bèta) Vorm dossier het formatteren opties voor op dossier-gebaseerde bestemmingen

>[!IMPORTANT]
>
>De **[!UICONTROL File formatting options]** in Adobe Experience Platform is momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.
>Neem contact op met uw Adobe-vertegenwoordiger voor toegang tot deze functie.
> 
>De opmaakopties voor bestanden die in dit document worden beschreven, zijn momenteel alleen beschikbaar voor CSV-bestanden.

De optie om verschillende opties voor de bestandsindeling van de geëxporteerde bestanden te configureren, is beschikbaar wanneer u [verbinden](/help/destinations/ui/connect-destination.md) naar een op een bestand gebaseerd doel, zoals [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect), of [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

U kunt verschillende opmaakopties voor geëxporteerde bestanden configureren met de interface van het Experience Platform. U kunt verschillende eigenschappen van de geëxporteerde bestanden aanpassen aan de vereisten van het systeem voor het ontvangen van bestanden aan uw zijde, zodat u de bestanden die u van het Experience Platform hebt ontvangen, optimaal kunt lezen en interpreteren.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuratie bestandsindeling {#file-configuration}

>[!IMPORTANT]
>
>Mogelijk zijn niet al deze opties beschikbaar voor de bestemming waarmee u verbinding maakt. Het is aan de bestemmingsontwikkelaar om te bepalen welke dossier het formatteren opties zij in hun bestemming willen steunen. De bestemmingsontwikkelaar kan bepalen welke opties beschikbaar zijn wanneer het verbinden met de bestemming. De vereiste opties zijn duidelijk met een asterisk in de UI van het Experience Platform.

Als u de opties voor de bestandsindeling wilt weergeven, start u de [verbinding maken met doel](/help/destinations/ui/connect-destination.md) workflow en selecteer segmenten als **Bestandstype**. In deze sectie worden de instellingen voor de bestandsindeling beschreven die beschikbaar zijn voor het geëxporteerde `CSV` bestanden.

![Afbeelding met enkele beschikbare opties voor bestandsindeling.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Scheidingsteken

Hiermee stelt u een scheidingsteken in voor elk veld en elke waarde. Bijvoorbeeld: `,` voor door komma&#39;s gescheiden waarden of `/t` voor tabgescheiden waarden.

### Aanhalingsteken

Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken van geciteerde waarden, waarbij het scheidingsteken deel kan uitmaken van de waarde.

### Escape-teken

Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken voor aanhalingstekens binnen een reeds geciteerde waarde.

### Uitvoer van lege waarde

Stelt de tekenreeksrepresentatie in van een lege waarde.

### Uitvoer van waarde Null

Hiermee stelt u de tekenreeksrepresentatie in van een waarde null in de geëxporteerde bestanden.

Voorbeeld van uitvoer met **[!UICONTROL null]** geselecteerd: `male,NULL,TestLastName`
Voorbeeld van uitvoer met **&quot;&quot;** geselecteerd: `male,"",TestLastName`
Voorbeeld van uitvoer met **[!UICONTROL Empty string]** geselecteerd: `male,,TestLastName`

### Compressie-indeling

Hiermee stelt u in welke compressiecodec moet worden gebruikt bij het opslaan van gegevens naar bestand. Ondersteunde opties zijn GZIP en NONE.

### Codering

*Niet weergegeven in de gebruikersinterfacescherm*. Hiermee wordt de codering (charset) van opgeslagen CSV-bestanden opgegeven. De opties zijn UTF-8 of UTF-16.

### Char om te ontsnappen aan aanhalingsteken

*Niet weergegeven in de gebruikersinterfacescherm*. Een markering die aangeeft of waarden die aanhalingstekens bevatten, altijd tussen aanhalingstekens moeten worden geplaatst.

Standaard worden alle waarden met een aanhalingsteken verwijderd.

### Lijnscheidingsteken

*Niet weergegeven in de gebruikersinterfacescherm*. Hiermee definieert u het lijnscheidingsteken dat moet worden gebruikt voor schrijven. De maximumlengte is 1 teken.

### Voorloopspatie negeren

*Niet weergegeven in de gebruikersinterfacescherm*. Een markering die aangeeft of witruimten die de regelafstand bepalen van waarden die worden geëxporteerd, moeten worden overgeslagen.

Voorbeeld van uitvoer met **[!UICONTROL True]** geselecteerd: `"male","John","TestLastName"`
Voorbeeld van uitvoer met **[!UICONTROL False]** geselecteerd: `" male","John","TestLastName"`

### Navolgende witruimte negeren

Niet weergegeven in de gebruikersinterfaceschermopname. Een vlag die aangeeft of overlopende witruimten van waarden die worden geëxporteerd, moeten worden overgeslagen.

Voorbeeld van uitvoer met **[!UICONTROL True]** geselecteerd: `"male","John","TestLastName"`
Voorbeeld van uitvoer met **[!UICONTROL False]** geselecteerd: `"male ","John","TestLastName"`

### Volgende stappen {#next-steps}

Na het lezen van dit document, weet u nu hoe te om dossieruitvoeropties voor uw Csv- gegevensdossiers te vormen om de dossierinhoud aan de vereisten van uw stroomafwaartse systeem van de dossierontvangst aan te passen. Vervolgens kunt u de [zelfstudie over activering van bestandsdoelen](/help/destinations/ui/activate-batch-profile-destinations.md) om bestanden naar de gewenste locatie voor cloudopslag te exporteren.
