---
title: Gebruik het laatste kwalificatietijd XDM attribuut in de nieuwe bètawolopslagbestemmingen
description: Leer hoe u het laatste XDM-attribuut voor kwalificatietijd in de nieuwe bètawolkenopslagbestemmingen gebruikt
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Gebruik het laatste kwalificatietijd XDM attribuut in de nieuwe bètawolopslagbestemmingen {#last-qualification-time}

>[!IMPORTANT]
> 
>Deze pagina beschrijft functionaliteit die in bèta is. De functionaliteit en documentatie kunnen worden gewijzigd. Neem contact op met uw Adobe of de klantenservice als u toegang wilt tot dit bètaprogramma.

## Vereisten {#prerequisites}

De laatste kwalificatietijd gebruiken (`lastQualificationTime`) XDM-kenmerk, moet u gegevens exporteren naar een van de zes hieronder vermelde cloudopslagdoelen:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Hoe te om de laatste kwalificatietijd XDM attributen te gebruiken {#how-to-use}

Als u een van de zes hierboven vermelde cloudopslagconnectors gebruikt, kunt u de laatste kwalificatietijd-XDM-attribuut in de [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) van de activeringsworkflow om een kolom in het geëxporteerde bestand te maken met de nieuwste tijdstempel van wanneer een profiel in aanmerking komt voor een segment. Dit kan u helpen bij het gebruik van bepaalde maateenheden of analysemogelijkheden en u een beter idee geven van wanneer u bepaalde soorten publiek moet activeren.

Opmerking: toevoegen `lastQualificationTime` naar het geëxporteerde bestand moet u de waarde momenteel handmatig invoegen `xdm: segmentMembership.ups.seg_id.lastQualificationTime` in het bronveld, zoals hieronder wordt weergegeven. U kunt het doelveld ook bewerken tot `lastQualificationTime` of een andere waarde die u deze kolom een naam wilt geven. Aangezien dit een bètafunctionaliteit is, is de syntaxis van de `xdm: segmentMembership.ups.seg_id.lastQualificationTime` De waarde kan in de toekomst veranderen.

![De opname die van het scherm het laatste attribuut van de kwalificatietijd XDM in de toewijzingsstap toont](/help/destinations/ui/last-qualification-time.gif)

## Meer informatie {#more-information}

Voor uitgebreide informatie over het activeren van gegevens aan op dossier-gebaseerde bestemmingen met inbegrip van alle stappen in het werkschema en noodzakelijke toestemmingen, lees [zelfstudie over op bestanden gebaseerde doelen activeren](/help/destinations/ui/activate-batch-profile-destinations.md).
