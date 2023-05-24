---
title: Gebruik het laatste kwalificatietijd XDM attribuut in de nieuwe bètawolopslagbestemmingen
description: Leer hoe u het laatste XDM-attribuut voor kwalificatietijd in de nieuwe bètawolkenopslagbestemmingen gebruikt
hidefromtoc: y
hide: y
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Gebruik het laatste kwalificatietijd XDM attribuut in de nieuwe bètawolopslagbestemmingen {#last-qualification-time}

>[!IMPORTANT]
> 
>Deze pagina beschrijft functionaliteit die in bèta is. De functionaliteit en documentatie kunnen worden gewijzigd. Neem contact op met uw Adobe-vertegenwoordiger of de klantenservice als u toegang wilt tot dit bètaprogramma.

## Vereisten {#prerequisites}

De laatste kwalificatietijd gebruiken (`lastQualificationTime`) XDM-kenmerk, moet u zijn ingeschreven voor het [bètaprogramma](/help/release-notes/2022/october-2022.md#destinations) om de verbeterde functionaliteit voor het exporteren van bestanden te gebruiken en gegevens te exporteren naar een van de zes [bètawolkenopslagdoelen](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). U bent ingeschreven als u de nieuwe bètakaarten voor de bestemmingen van de wolkenopslag in de catalogus kunt zien, zoals hieronder getoond voor [!DNL Amazon S3].

![Afbeelding van de nieuwe Amazon S3-bèta-kaart](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## Hoe te om de laatste kwalificatietijd XDM attributen te gebruiken {#how-to-use}

Als u een van de zes nieuwe bètaconnectors voor cloudopslag gebruikt, kunt u het laatste XDM-attribuut voor kwalificatietijd in het dialoogvenster [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) van de activeringsworkflow om een kolom in het geëxporteerde bestand te maken met de nieuwste tijdstempel van wanneer een profiel in aanmerking komt voor een segment. Dit kan u helpen bij het gebruik van bepaalde maateenheden of analysemogelijkheden en u een beter idee geven van wanneer u bepaalde soorten publiek moet activeren.

Opmerking: toevoegen `lastQualificationTime` naar het geëxporteerde bestand moet u de waarde momenteel handmatig invoegen `xdm: segmentMembership.ups.seg_id.lastQualificationTime` in het bronveld, zoals hieronder wordt weergegeven. U kunt het doelveld ook bewerken naar `lastQualificationTime` of een andere waarde die u deze kolom een naam wilt geven. Aangezien dit een bètafunctionaliteit is, is de syntaxis van de `xdm: segmentMembership.ups.seg_id.lastQualificationTime` De waarde kan in de toekomst veranderen.

![De opname die van het scherm het laatste attribuut van de kwalificatietijd XDM in de toewijzingsstap toont](/help/destinations/ui/last-qualification-time.gif)

## Meer informatie {#more-information}

Voor uitgebreide informatie over het activeren van gegevens aan op dossier-gebaseerde bestemmingen met inbegrip van alle stappen in het werkschema en noodzakelijke toestemmingen, lees [zelfstudie over op bestanden gebaseerde doelen activeren](/help/destinations/ui/activate-batch-profile-destinations.md).
