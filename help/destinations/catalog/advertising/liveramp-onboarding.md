---
title: LiveRamp - Verbinding aan boord
description: Leer hoe u de LiveRamp-aansluiting kunt gebruiken voor het on-board publiek van Adobe Real-Time Customer Data Platform naar LiveRamp Connect.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: b8540eb20838e7f2228d71bfc002392d07daffe4
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 0%

---

# [!DNL LiveRamp - Onboarding]-verbinding {#liveramp-onboarding}

Gebruik de [!DNL LiveRamp - Onboarding] -verbinding met het on-board publiek van Adobe Real-Time Customer Data Platform naar [!DNL LiveRamp Connect] .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL LiveRamp - Onboarding] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

Als markator wil ik een publiek van Adobe Experience Platform naar boordidentiteiten sturen naar [!DNL LiveRamp Connect] , zodat ik gebruikers op mobiele, open web-, sociale en [!DNL CTV] -platforms kan besturen met de id [!DNL Ramp ID] .

## Vereisten {#prerequisites}

De [!DNL LiveRamp - Onboarding] verbinding voert dossiers uit gebruikend [ 2} opslag van SFTP van LiveRamp {.](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html)

Voordat u gegevens van Experience Platform naar [!DNL LiveRamp - Onboarding] kunt verzenden, hebt u uw [!DNL LiveRamp] -referenties nodig. Neem contact op met uw [!DNL LiveRamp] -vertegenwoordiger om uw referenties te verkrijgen, als u deze nog niet hebt.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LiveRamp - Onboarding] steunt de activering van identiteiten zoals op PII-Gebaseerde herkenningstekens, bekende herkenningstekens, en douane IDs, die in de officiële [ documentatie LiveRamp ](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers) wordt beschreven.

In de [ toewijzingsstap ](#map) van het activeringswerkschema, moet u de doelafbeeldingen als douanekenmerken bepalen.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL LiveRamp - Onboarding] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Batch]** | Aangezien profielen in Experience Platform worden bijgewerkt op basis van publieksevaluatie, worden de profielen (identiteiten) bijgewerkt en kunnen stroomafwaarts worden geleverd aan het doelplatform op een dagelijkse, wekelijkse of maandelijkse frequentie. Lees meer over [ partij op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

**authentificatie SFTP met wachtwoord** {#sftp-password}

![ het schermschot van de Steekproef die hoe te om aan de bestemming voor authentiek te verklaren gebruikend SFTP met wachtwoord ](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png) tonen

* **[!UICONTROL Port]**: De poort die wordt gebruikt voor de opslaglocatie van [!DNL LiveRamp - Onboarding] .  Gebruik de poort die overeenkomt met uw geografische locatie, zoals hieronder wordt beschreven:
   * **[!UICONTROL NA]**: poort gebruiken `22`
   * **[!UICONTROL AU]**: poort gebruiken `2222`
* **[!UICONTROL Username]**: De gebruikersnaam voor de opslaglocatie van [!DNL LiveRamp - Onboarding] .
* **[!UICONTROL Password]**: Het wachtwoord voor de opslaglocatie van [!DNL LiveRamp - Onboarding] .
* **[!UICONTROL PGP/GPG encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.
  ![ Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont ](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey ID]**:Ifwanneer u een coderingssleutel opgeeft, moet u ook een codering opgeven **[!UICONTROL Subkey ID]**. Zie [!DNL LiveRamp] [ encryptiedocumentatie ](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) leren hoe te om subkey identiteitskaart te verkrijgen.

**SFTP met SSH zeer belangrijke authentificatie** {#sftp-ssh}

![ het schermschot van de Steekproef die hoe te om aan de bestemming voor authentiek te verklaren gebruikend sleutel SSH ](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png) tonen

* **[!UICONTROL Port]**: De poort die wordt gebruikt voor de opslaglocatie van [!DNL LiveRamp - Onboarding] .  Gebruik de poort die overeenkomt met uw geografische locatie, zoals hieronder wordt beschreven:
   * **[!UICONTROL EU]**: poort gebruiken `4222`
* **[!UICONTROL Username]**: De gebruikersnaam voor de opslaglocatie van [!DNL LiveRamp - Onboarding] .
* **[!UICONTROL SSH Key]**: De persoonlijke [!DNL SSH] -sleutel die wordt gebruikt om u aan te melden bij uw [!DNL LiveRamp - Onboarding] -opslaglocatie. De persoonlijke sleutel moet zijn opgemaakt als een [!DNL Base64] -gecodeerde tekenreeks en mag niet met een wachtwoord zijn beveiligd.

   * Als u de [!DNL SSH] -sleutel wilt koppelen aan de [!DNL LiveRamp - Onboarding] -server, moet u een ticket verzenden via de portal voor technische ondersteuning van [!DNL LiveRamp] en uw openbare sleutel opgeven. Zie meer informatie in de [ documentatie LiveRamp ](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL PGP/GPG encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.
  ![ Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont ](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey ID]**:Ifwanneer u een coderingssleutel opgeeft, moet u ook een codering opgeven **[!UICONTROL Subkey ID]**. Zie [!DNL LiveRamp] [ encryptiedocumentatie ](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) leren hoe te om subkey identiteitskaart te verkrijgen.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="Id van coderingssubsleutel"
>abstract="De subsleutel-id die voor codering wordt gebruikt, op basis van de openbare coderingssleutel van LiveRamp. Dit gebied wordt vereist als u een encryptiesleutel in de authentificatiestap verstrekte."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Leer hoe u de subsleutel-id verkrijgt"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

{het schermschot van 0} Experience Platform UI die tonen hoe te om details voor uw bestemming in te vullen ![](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Region]**: Geografisch gebied voor uw instantie van de LiveRamp SFTP-opslag.
* **[!UICONTROL Folder path]**: Het pad naar de submap [!DNL LiveRamp] `uploads` die de geëxporteerde bestanden host. Het voorvoegsel `uploads` wordt automatisch toegevoegd aan het mappad. [!DNL LiveRamp] raadt u aan een speciale submap voor leveringen van Adobe Real-Time CDP te maken om de bestanden gescheiden te houden van andere bestaande feeds en om ervoor te zorgen dat alle automatisering probleemloos wordt uitgevoerd.
   * Als u bijvoorbeeld uw bestanden naar `uploads/my_export_folder` wilt exporteren, typt u in `my_export_folder` in het veld **[!UICONTROL Folder path]** .
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden. Beschikbare opties zijn **[!UICONTROL GZIP]** of **[!UICONTROL None]** .

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, lees de gids over [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [ activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Planning {#scheduling}

Maak in de stap [!UICONTROL Scheduling] een exportschema voor elk publiek met de onderstaande instellingen.

* **[!UICONTROL File export options]**: [!UICONTROL Export full files] . [ de Incrementele dossieruitvoer ](../../ui/activate-batch-profile-destinations.md#export-incremental-files) wordt momenteel niet gesteund voor de [!DNL LiveRamp] bestemming.
* **[!UICONTROL Frequency]**: [!UICONTROL Daily] , [!UICONTROL Weekly] of [!UICONTROL Monthly]
* **[!UICONTROL Date]**: selecteer de begin- en eindtijd van het exporteren naar wens.

{het schermschot van 0} Experience Platform UI die het publiek toont die stap plannen.![](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

De geëxporteerde bestandsnaam kan momenteel niet door de gebruiker worden geconfigureerd. Alle bestanden die naar de [!DNL LiveRamp - Onboarding] -bestemming worden geëxporteerd, krijgen automatisch een naam op basis van de volgende sjabloon:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

{het schermschot van 0} Experience Platform UI die het uitgevoerde dossier - naammalplaatje toont.![](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

De naam van een geëxporteerd bestand voor een organisatie met de naam [!DNL Luma] kan er bijvoorbeeld als volgt uitzien:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Kenmerken en identiteiten toewijzen {#map}

In de stap **[!UICONTROL Mapping]** kunt u selecteren welke kenmerken en identiteiten u wilt exporteren voor uw profielen.

>[!IMPORTANT]
>
>Deze bestemming ondersteunt de activering van één naamruimte van de bronidentiteit per activeringsstroom. Als u veelvoudige identiteit namespaces, als `Email` en `Phone` moet uitvoeren, moet u [ een afzonderlijke activeringsstroom ](../../ui/activate-batch-profile-destinations.md) voor elke identiteit creëren.

In de stap **[!UICONTROL Mapping]** definieert de toewijzing **[!UICONTROL Target field]** de naam van de kolomkop in het geëxporteerde CSV-bestand. U kunt de CSV-kolomkoppen in het geëxporteerde bestand wijzigen in elke gewenste vriendelijke naam door een aangepaste naam op te geven voor de **[!UICONTROL Target field]** .

>[!IMPORTANT]
>
>Voor om het even welke veranderingen die aan de doelgebieden na uw aanvankelijke dossierlevering aan [!DNL LiveRamp] worden aangebracht, te informeren gelieve uw [!DNL LiveRamp] accountteam of [ een kaartje aan Steun LiveRamp ](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case) voorleggen om ervoor te zorgen dat de veranderingen in het automatiseringsproces worden weerspiegeld.

1. Selecteer **[!UICONTROL Mapping]** in de stap **[!UICONTROL Add new mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.

   ![ de schermopname van Experience Platform UI die het scherm van de Afbeelding toont.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk dat u wilt toewijzen, of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer de identiteit die u wilt toewijzen aan uw doel.

   ![ het schermschot van Experience Platform UI die het scherm van de bronToewijzing toont.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. Voer in het venster **[!UICONTROL Select target field]** de kenmerknaam in waaraan u het geselecteerde bronveld wilt toewijzen. De hier gedefinieerde kenmerknaam wordt in het geëxporteerde CSV-bestand weergegeven als kolomkop.

   ![ de screeshot van Experience Platform UI die het scherm van het doelToewijzing toont.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   U kunt de kenmerknaam ook invoeren door deze rechtstreeks in **[!UICONTROL Target field]** te typen.

   ![ de screeshot van Experience Platform UI die het scherm van het doelToewijzing toont.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

Nadat u alle gewenste toewijzingen hebt toegevoegd, selecteert u **[!UICONTROL Next]** en voltooit u de activeringsworkflow.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Uw gegevens worden als CSV-bestanden geëxporteerd naar de opslaglocatie van [!DNL LiveRamp - Onboarding] die u hebt geconfigureerd.

Geëxporteerde bestanden hebben een maximale grootte van 10 miljoen rijen. Experience Platform genereert meerdere bestanden per levering als het geselecteerde publiek groter is dan 10 miljoen rijen. Als u verwacht dat u de limiet voor één bestand overschrijdt, neemt u contact op met uw [!DNL LiveRamp] -vertegenwoordiger en vraagt u deze om batch-opname voor u te configureren.

Wanneer het uitvoeren van dossiers aan de [!DNL LiveRamp - Onboarding] bestemming, produceert Experience Platform één Csv- dossier voor elke [ identiteitskaart van het fusiebeleid ](../../../profile/merge-policies/overview.md).

Neem bijvoorbeeld het volgende publiek:

* Publiek A (Samenvoegingsbeleid 1)
* Publiek B (Samenvoegingsbeleid 2)
* Publiek C (Samenvoegingsbeleid 1)
* Publiek D (Samenvoegingsbeleid 1)

Experience Platform exporteert twee CSV-bestanden naar [!DNL LiveRamp - Onboarding] :

* één CSV-bestand met soorten publiek A, C en D;
* Eén CSV-bestand met publiek B.

Geëxporteerde CSV-bestanden bevatten profielen met de geselecteerde kenmerken en de corresponderende publieksstatus, in afzonderlijke kolommen, met de kenmerknaam en `audience_namespace:audience_ID` paren als kolomkoppen, zoals in het onderstaande voorbeeld wordt getoond:

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1_AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2_AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X_AUDIENCE_ID_X`

De profielen in de geëxporteerde bestanden kunnen overeenkomen met een van de volgende kwalificatiestatus van het publiek:

* `Active`: Het profiel is momenteel gekwalificeerd voor het publiek.
* `Expired`: het profiel is niet langer gekwalificeerd voor het publiek, maar is in het verleden wel gekwalificeerd.
* `""` (lege tekenreeks): Het profiel wordt nooit in aanmerking genomen voor het publiek.

Bijvoorbeeld, een uitgevoerd CSV dossier met één `email` attribuut, twee publiek uit de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md) voortkomt, en één [ ingevoerd ](../../../segmentation/ui/audience-portal.md#import-audience) extern publiek, kon als dit kijken:

```csv
email,ups_aa2e3d98-974b-4f8b-9507-59f65b6442df,ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

In het voorbeeld hierboven, beschrijven de `ups_aa2e3d98-974b-4f8b-9507-59f65b6442df` en `ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` secties publiek dat uit de Dienst van de Segmentatie voortkomt, terwijl `CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e` een publiek beschrijft dat in Experience Platform als a [ wordt ingevoerd uploadt ](../../../segmentation/ui/audience-portal.md#import-audience).

Aangezien Experience Platform één Csv- dossier voor elke [ identiteitskaart van het fusiebeleid ](../../../profile/merge-policies/overview.md) produceert, produceert het ook een afzonderlijke dataflow looppas voor elke identiteitskaart van het fusiebeleid.

Dit betekent dat de **[!UICONTROL Identities activated]** en **[!UICONTROL Profiles received]** metriek in de [ dataflow looppas ](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) pagina voor elke groep van publiek worden samengevoegd die het zelfde fusiebeleid gebruiken, in plaats van wordt getoond voor elk publiek.

Als gevolg van dataflow looppas die voor een groep van publiek wordt geproduceerd die het zelfde fusiebeleid gebruiken, worden de publieksnamen niet getoond in het [ controledashboard ](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![ het schermopname van Experience Platform UI die de metrisch geactiveerde identiteiten toont.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## Geëxporteerde gegevens uploaden naar LiveRamp {#upload-to-liveramp}

Nadat uw gegevens naar de [!DNL LiveRamp - Onboarding] -opslag zijn geëxporteerd, moet u de gegevens uploaden naar het [!DNL LiveRamp] -platform.

Voor meer informatie over hoe te om uw dossiers van de [!DNL LiveRamp - Onboarding] opslag aan een [!DNL LiveRamp] publiek te uploaden, zie de volgende documentatie: [ Overwegingen wanneer het Uploaden van het Eerste Dossier aan een Publiek ](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Voor meer details op hoe te om uw [!DNL LiveRamp - Onboarding] opslag te vormen, zie de [ officiële documentatie ](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).

## Changelog {#changelog}

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Februari 2025 | Bijwerken van functionaliteit en documentatie | <ul><li> Extra ondersteuning voor wekelijkse en maandelijkse leveringskadences. |
| Maart 2024 | Bijwerken van functionaliteit en documentatie | <ul><li>Extra ondersteuning voor leveringen aan instanties van Europa en Australië [!DNL LiveRamp] [!DNL SFTP] .</li><li>Bijgewerkte documentatie om specifieke configuraties voor onlangs gesteunde gebieden te beschrijven.</li><li>Maximale bestandsgrootte is verhoogd tot 10 miljoen rijen (van 5 miljoen, eerder).</li><li>Bijgewerkte documentatie die op verhoogde dossiergrootte wijst.</li></ul> |
| Juli 2023 | Eerste release | Eerste doelversie en documentatie gepubliceerd. |

{style="table-layout:auto"}

+++
