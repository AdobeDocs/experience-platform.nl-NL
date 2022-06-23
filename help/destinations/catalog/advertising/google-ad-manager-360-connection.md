---
title: (bèta) [!DNL Google Ad Manager 360] verbinding
description: Google Ad Manager 360 is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# (bèta) [!DNL Google Ad Manager 360] verbinding

## Overzicht {#overview}

De [!DNL Google Ad Manager 360] verbinding maakt batch-upload mogelijk voor [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Voor meer informatie over hoe de uitgever verstrekte herkenningstekens in Google Ad Manager 360 werkt, zie [officiële Google-documentatie](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Deze bestemming is momenteel in Bèta en is slechts beschikbaar aan een beperkt aantal klanten. Om toegang tot [!DNL Google Ad Manager 360] verbinding, neem contact op met uw Adobe-vertegenwoordiger en geef uw [!DNL IMS Organization ID].

De [!DNL Google Ad Manager 360] doelexport [!DNL CSV] bestanden naar uw [!DNL Google Cloud Storage] emmertje. Als u de [!DNL CSV] bestanden, moet u deze importeren in uw [!DNL Google Ad Manager 360] account.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager 360] bestemmingen.

* Geactiveerd publiek wordt met programmacode gemaakt in het Google-platform en gevuld in het CSV-bestand.

## Ondersteunde identiteiten {#supported-identities}

[!DNL This integration] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selecteer deze doelidentiteit om het publiek naar te sturen [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Vereisten {#prerequisites}

### Aanbieding toestaan {#allow-listing}

>[!NOTE]
>
>De lijst van gewenste personen is verplicht voordat u de eerste [!DNL Google Ad Manager] bestemming in Platform. Controleer of de hieronder beschreven lijst van gewenste personen is voltooid door [!DNL Google] voordat u een doel maakt.

Voordat u het dialoogvenster [!DNL Google Ad Manager 360] bestemming in Platform, moet u contact opnemen [!DNL Google] voor Adobe die op de lijst met toegestane gegevensproviders moet worden geplaatst, en dat uw account aan de lijst van gewenste personen wordt toegevoegd. Contact [!DNL Google] en verstrekt de volgende informatie:

* **Account-id**: De account-id van Adobe met Google. Account-id: 87933855.
* **Klant-id**: De klant-id van Adobe met Google. Klant-id: 89690775.
* **Netwerk-id**: dit is je account met [!DNL Google Ad Manager]
* **Koppeling-id voor publiek**: dit is je account met [!DNL Google Ad Manager]
* Je accounttype. DFP door Google of AdX koper.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Bucket name]**: Voer de naam in van de [!DNL Google Cloud Storage] emmer die door deze bestemming moet worden gebruikt.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

In de stap voor identiteitstoewijzing kunt u de volgende vooraf ingevulde toewijzingen zien:

| Vooraf ingevulde toewijzing | Beschrijving |
|---------|----------|
| `ECID` -> `ppid` | Dit is de enige door de gebruiker bewerkbare vooraf ingevulde toewijzing. U kunt al uw kenmerken of naamruimten selecteren in het Platform en deze toewijzen aan `ppid`. |
| `metadata.segment.alias` -> `list_id` | Hiermee kunt u segmentnamen van Experience Platforms toewijzen aan segment-id&#39;s in het Google-platform. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Vertelt het Google-platform wanneer gediskwalificeerde gebruikers uit segmenten moeten worden verwijderd. |

Deze toewijzingen zijn vereist door [!DNL Google Ad Manager 360] en worden automatisch door Adobe Experience Platform voor iedereen gemaakt [!DNL Google Ad Manager 360] verbindingen.

![UI-afbeelding die de toewijzingsstap voor Google Ad Manager 360 weergeeft.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Google Cloud Storage] emmertje en zorg ervoor de uitgevoerde dossiers de verwachte profielpopulaties bevatten.
