---
title: LiveRamp - Verbinding aan boord
description: Leer hoe u de LiveRamp-aansluiting kunt gebruiken voor het on-board publiek van Adobe Real-time Customer Data Platform naar LiveRamp Connect.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: a235f9a66ea15fc5e72dd6ed03e4a6a384fd30a4
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 0%

---

# [!DNL LiveRamp - Onboarding] verbinding {#liveramp-onboarding}

Gebruik de [!DNL LiveRamp - Onboarding] verbinding met het on-board publiek van Adobe Real-time Customer Data Platform naar [!DNL LiveRamp Connect].

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL LiveRamp - Onboarding] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

Als marketeer wil ik een publiek van Adobe Experience Platform naar boordidentiteiten sturen naar [!DNL LiveRamp Connect] zodat ik gebruikers op mobiel, open Web, sociaal kan richten en [!DNL CTV] platformen, gebruiken [!DNL Ramp ID] id.

## Vereisten {#prerequisites}

De [!DNL LiveRamp - Onboarding] verbinding exporteert bestanden met [SFTP van LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) opslag.

Voordat u gegevens van het Experience Platform kunt verzenden naar [!DNL LiveRamp - Onboarding], hebt u uw [!DNL LiveRamp] referenties. Neem contact op met uw [!DNL LiveRamp] om uw geloofsbrieven te verkrijgen, als u niet reeds hebt.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LiveRamp - Onboarding] ondersteunt de activering van identiteiten zoals op PII gebaseerde id&#39;s, bekende id&#39;s en aangepaste id&#39;s, zoals beschreven in de officiële [LiveRamp-documentatie](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

In de [toewijzingsstap](#map) van de activeringsworkflow moet u de doeltoewijzingen definiëren als aangepaste kenmerken.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster [!DNL LiveRamp - Onboarding] bestemming. |
| Exportfrequentie | **[!UICONTROL Daily batch]** | Aangezien de profielen in Experience Platform op publieksevaluatie worden bijgewerkt, worden de profielen (identiteiten) bijgewerkt eens per dag stroomafwaarts aan het bestemmingsplatform. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

**SFTP-verificatie met wachtwoord** {#sftp-password}

![Voorbeeldschermafbeelding die laat zien hoe u de bestemming verifieert met gebruik van SFTP met wachtwoord](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL Port]**: De poort die voor uw [!DNL LiveRamp - Onboarding] opslaglocatie.  Gebruik de poort die overeenkomt met uw geografische locatie, zoals hieronder wordt beschreven:
   * **[!UICONTROL NA]**: poort gebruiken `22`
   * **[!UICONTROL AU]**: poort gebruiken `2222`
* **[!UICONTROL Username]**: De gebruikersnaam voor uw [!DNL LiveRamp - Onboarding] opslaglocatie.
* **[!UICONTROL Password]**: Het wachtwoord voor uw [!DNL LiveRamp - Onboarding] opslaglocatie.
* **[!UICONTROL PGP/GPG encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.
  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey ID]**:Als u een coderingssleutel opgeeft, moet u ook een codering opgeven **[!UICONTROL Subkey ID]**. Zie de [!DNL LiveRamp] [versleutelingsdocumentatie](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) om te leren hoe te om subkey identiteitskaart te verkrijgen

**SFTP met SSH-sleutelverificatie** {#sftp-ssh}

![Voorbeeldschermafbeelding die aangeeft hoe u de bestemming kunt verifiëren met behulp van de SSH-toets](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL Port]**: De poort die voor uw [!DNL LiveRamp - Onboarding] opslaglocatie.  Gebruik de poort die overeenkomt met uw geografische locatie, zoals hieronder wordt beschreven:
   * **[!UICONTROL EU]**: poort gebruiken `4222`
* **[!UICONTROL Username]**: De gebruikersnaam voor uw [!DNL LiveRamp - Onboarding] opslaglocatie.
* **[!UICONTROL SSH Key]** Betreft: Particulier [!DNL SSH] sleutel die wordt gebruikt om aan te melden bij uw [!DNL LiveRamp - Onboarding] opslaglocatie. De persoonlijke sleutel moet als een [!DNL Base64]-coded string en mag niet met een wachtwoord beveiligd zijn.

   * Als u verbinding wilt maken met uw [!DNL SSH] sleutel tot de [!DNL LiveRamp - Onboarding] server, moet u een kaartje door indienen [!DNL LiveRamp]Het portal voor technische ondersteuning en uw openbare sleutel. Meer informatie vindt u in het dialoogvenster [LiveRamp-documentatie](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL PGP/GPG encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.
  ![Afbeelding met een voorbeeld van een PGP-sleutel met de juiste notatie in de gebruikersinterface](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey ID]**:Als u een coderingssleutel opgeeft, moet u ook een codering opgeven **[!UICONTROL Subkey ID]**. Zie de [!DNL LiveRamp] [versleutelingsdocumentatie](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) om te leren hoe te om subkey identiteitskaart te verkrijgen

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="Id van coderingssubsleutel"
>abstract="De subsleutel-id die voor codering wordt gebruikt, op basis van de openbare coderingssleutel van LiveRamp. Dit gebied wordt vereist als u een encryptiesleutel in de authentificatiestap verstrekte."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Leer hoe u de subsleutel-id verkrijgt"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Schermopname van de UI van het platform die tonen hoe te om details voor uw bestemming in te vullen](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Region]**: Geografisch gebied voor uw instantie van de LiveRamp SFTP-opslag.
* **[!UICONTROL Folder path]**: Het pad naar de [!DNL LiveRamp] `uploads` submap die de geëxporteerde bestanden host. De `uploads` wordt automatisch toegevoegd aan het mappad. [!DNL LiveRamp] Het verdient aanbeveling een speciale submap voor leveringen van Adobe Real-Time CDP te maken om de bestanden gescheiden te houden van andere bestaande feeds en om ervoor te zorgen dat alle automatisering probleemloos wordt uitgevoerd.
   * Als u bijvoorbeeld uw bestanden wilt exporteren naar `uploads/my_export_folder`, typt u `my_export_folder` in de **[!UICONTROL Folder path]** veld.
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden. Beschikbare opties zijn **[!UICONTROL GZIP]** of **[!UICONTROL None]**.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Lees voor meer informatie over waarschuwingen de handleiding op [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Planning {#scheduling}

In de [!UICONTROL Scheduling] Maak een exportschema voor elk publiek met de onderstaande instellingen.

* **[!UICONTROL File export options]**: [!UICONTROL Export full files]. [Incrementele bestandsuitvoer](../../ui/activate-batch-profile-destinations.md#export-incremental-files) worden momenteel niet ondersteund voor de [!DNL LiveRamp] bestemming.
* **[!UICONTROL Frequency]**: [!UICONTROL Daily]
* **[!UICONTROL Date]**: Selecteer de begin- en eindtijd van het exporteren naar wens.

![Schermopname van de gebruikersinterface van het platform die de publiek plannende stap toont.](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

De geëxporteerde bestandsnaam kan momenteel niet door de gebruiker worden geconfigureerd. Alle bestanden die naar de [!DNL LiveRamp - Onboarding] de bestemming wordt automatisch genoemd gebaseerd op het volgende malplaatje:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Platform UI-screenshot met de geëxporteerde bestandsnaamsjabloon.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

De naam van een geëxporteerd bestand voor een organisatie met de naam [!DNL Luma] kan er ongeveer als volgt uitzien :

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Kenmerken en identiteiten toewijzen {#map}

In de **[!UICONTROL Mapping]** kunt u kiezen welke kenmerken en identiteiten u wilt exporteren voor uw profielen.

>[!IMPORTANT]
>
>Deze bestemming ondersteunt de activering van één naamruimte van de bronidentiteit per activeringsstroom. Als u meerdere naamruimten wilt exporteren, bijvoorbeeld `Email` en `Phone`, moet u [een aparte activeringsstroom maken](../../ui/activate-batch-profile-destinations.md) voor elke identiteit.

In de **[!UICONTROL Mapping]** de **[!UICONTROL Target field]** Met toewijzing wordt de naam van de kolomkop in het geëxporteerde CSV-bestand gedefinieerd. U kunt de CSV-kolomkoppen in het geëxporteerde bestand wijzigen in elke gewenste vriendelijke naam door een aangepaste naam op te geven voor de **[!UICONTROL Target field]**.

>[!IMPORTANT]
>
>Voor alle wijzigingen die u na de eerste bestandslevering in de doelvelden hebt aangebracht [!DNL LiveRamp], gelieve uw [!DNL LiveRamp] accountteam of [een ticket verzenden naar LiveRamp Support](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case) om ervoor te zorgen dat de wijzigingen in het automatiseringsproces tot uiting komen.

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.

   ![UI-screeshot van Experience Platform met het scherm Toewijzing.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk dat u wilt toewijzen of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit om toe te wijzen aan uw bestemming.

   ![UI-screeshot van Experience Platform met het scherm voor brontoewijzing.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. In de **[!UICONTROL Select target field]** Voer de kenmerknaam in waaraan u het geselecteerde bronveld wilt toewijzen. De hier gedefinieerde kenmerknaam wordt in het geëxporteerde CSV-bestand weergegeven als kolomkop.

   ![UI-screeshot van Experience Platform met het scherm voor het toewijzen van doelen.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   U kunt de kenmerknaam ook invoeren door deze rechtstreeks in te voeren in het dialoogvenster **[!UICONTROL Target field]**.

   ![UI-screeshot van Experience Platform met het scherm voor het toewijzen van doelen.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

Als u al uw gewenste toewijzingen hebt toegevoegd, selecteert u **[!UICONTROL Next]** en voltooi de activeringsworkflow.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Uw gegevens worden naar de [!DNL LiveRamp - Onboarding] opslaglocatie die u hebt geconfigureerd, als CSV-bestanden.

Geëxporteerde bestanden hebben een maximale grootte van 10 miljoen rijen. Experience Platform genereert meerdere bestanden per levering als het geselecteerde publiek groter is dan 10 miljoen rijen. Neem contact op met uw [!DNL LiveRamp] en vragen om batch-opname voor u te configureren.

Wanneer u bestanden exporteert naar de [!DNL LiveRamp - Onboarding] doel, Platform genereert één CSV-bestand voor elk [beleids-id samenvoegen](../../../profile/merge-policies/overview.md).

Neem bijvoorbeeld het volgende publiek:

* Publiek A (Samenvoegingsbeleid 1)
* Publiek B (Samenvoegingsbeleid 2)
* Publiek C (Samenvoegingsbeleid 1)
* Publiek D (Samenvoegingsbeleid 1)

Platform exporteert twee CSV-bestanden naar [!DNL LiveRamp - Onboarding]:

* één CSV-bestand met soorten publiek A, C en D;
* Eén CSV-bestand met publiek B.

Geëxporteerde CSV-bestanden bevatten profielen met de geselecteerde kenmerken en de corresponderende publieksstatus, in afzonderlijke kolommen en met de kenmerknaam, en `audience_namespace:audience_ID` paren als kolomkoppen, zoals in het onderstaande voorbeeld wordt getoond:

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1_AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2_AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X_AUDIENCE_ID_X`

De profielen in de geëxporteerde bestanden kunnen overeenkomen met een van de volgende kwalificatiestatus van het publiek:

* `Active`: Het profiel is momenteel gekwalificeerd voor het publiek.
* `Expired`: Het profiel is niet langer gekwalificeerd voor het publiek, maar is in het verleden wel gekwalificeerd.
* `""`(lege tekenreeks): Het profiel wordt nooit in aanmerking genomen voor het publiek.

Bijvoorbeeld een geëxporteerd CSV-bestand met één `email` kenmerk, twee soorten publiek afkomstig uit de Experience Platform [Segmenteringsservice](../../../segmentation/home.md), en één [geïmporteerd](../../../segmentation/ui/overview.md#importing-an-audience) extern publiek, zou als volgt kunnen kijken:

```csv
email,ups_aa2e3d98-974b-4f8b-9507-59f65b6442df,ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

In het bovenstaande voorbeeld wordt `ups_aa2e3d98-974b-4f8b-9507-59f65b6442df` en `ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` de secties beschrijven publiek dat uit de Dienst van de Segmentatie voortkomt, terwijl `CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e` beschrijft een publiek dat in Platform is geïmporteerd als een [aangepaste upload](../../../segmentation/ui/overview.md#importing-an-audience).

Aangezien Platform één CSV-bestand genereert voor elk bestand [beleids-id samenvoegen](../../../profile/merge-policies/overview.md), produceert het ook een afzonderlijke dataflow looppas voor elke identiteitskaart van het fusiebeleid.

Dit betekent dat de **[!UICONTROL Identities activated]** en **[!UICONTROL Profiles received]** maatstaven in de [dataflow-run](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) De pagina wordt samengevoegd voor elke groep publiek die het zelfde fusiebeleid gebruiken, in plaats van wordt getoond voor elk publiek.

Als gevolg van dataflow-run die wordt gegenereerd voor een groep soorten publiek die hetzelfde samenvoegbeleid gebruiken, worden de publieksnamen niet weergegeven in het dialoogvenster [controledashboard](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![UI-screeshot van Experience Platform met de metrische id die is geactiveerd.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## Geëxporteerde gegevens uploaden naar LiveRamp {#upload-to-liveramp}

Nadat uw gegevens naar de [!DNL LiveRamp - Onboarding] opslag, moet u de gegevens uploaden naar [!DNL LiveRamp] platform.

Voor meer informatie over het uploaden van uw bestanden vanuit de [!DNL LiveRamp - Onboarding] opslag in een [!DNL LiveRamp] publiek, zie de volgende documentatie: [Overwegingen bij het uploaden van het eerste bestand naar een publiek](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Voor meer details over hoe te om uw te vormen [!DNL LiveRamp - Onboarding] opslaan, zie de [officiële documentatie](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).

## Changelog {#changelog}

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Maart 2024 | Bijwerken van functionaliteit en documentatie | <ul><li>Toegevoegde steun voor leveringen aan Europa en Australië [!DNL LiveRamp] [!DNL SFTP] instanties.</li><li>Bijgewerkte documentatie om specifieke configuraties voor onlangs gesteunde gebieden te beschrijven.</li><li>Maximale bestandsgrootte is verhoogd tot 10 miljoen rijen (van 5 miljoen, eerder).</li><li>Bijgewerkte documentatie die op verhoogde dossiergrootte wijst.</li></ul> |
| Juli 2023 | Eerste release | Eerste doelversie en documentatie gepubliceerd. |

{style="table-layout:auto"}

+++
