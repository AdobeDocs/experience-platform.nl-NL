---
title: Gebruik het laatste kwalificatietijd XDM attribuut in de nieuwe bètawolopslagbestemmingen
description: Leer hoe u het laatste XDM-attribuut voor kwalificatietijd in de nieuwe bètawolkenopslagbestemmingen gebruikt
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Gebruik het laatste kwalificatietijd XDM attribuut in de nieuwe bètawolopslagbestemmingen {#last-qualification-time}

>[!IMPORTANT]
>
>Deze pagina beschrijft functionaliteit die in bèta is. De functionaliteit en documentatie kunnen worden gewijzigd. Neem contact op met uw Adobe-vertegenwoordiger of de klantenservice als u toegang wilt tot dit bètaprogramma.

## Vereisten {#prerequisites}

Om de laatste kwalificatietijd (`lastQualificationTime`) XDM attribuut te gebruiken, moet u gegevens naar één van de zes hieronder vermelde bestemmingen van de wolkenopslag uitvoeren:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zone]](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Hoe te om de laatste kwalificatietijd XDM attributen te gebruiken {#how-to-use}

Als u één van de zes hierboven vermelde schakelaars van de wolkenopslag gebruikt, kunt u de laatste attributen van de kwalificatietijd XDM in de [&#x200B; toewijzingsstap &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) van het activeringswerkschema gebruiken om een kolom in het uitgevoerde dossier met recentste timestamp van te creëren wanneer een profiel voor een segment kwalificeerde. Dit kan u helpen bij het gebruik van bepaalde maateenheden of analysemogelijkheden en u een beter idee geven van wanneer u bepaalde soorten publiek moet activeren.

>[!NOTE]
>
>Als u `lastQualificationTime` wilt toevoegen aan het exporteren van een bestand, moet u de waarde `xdm: segmentMembership.ups.seg_id.lastQualificationTime` momenteel handmatig in het bronveld invoegen, zoals hieronder wordt weergegeven. U kunt het doelveld ook bewerken in `lastQualificationTime` of een andere waarde die u een naam voor deze kolom wilt geven. Aangezien dit een bètafunctionaliteit is, kan de syntaxis van de `xdm: segmentMembership.ups.seg_id.lastQualificationTime` -waarde in de toekomst veranderen.

![&#x200B; het registreren van het Scherm die de laatste attribuut van de kwalificatietijdXDM in de afbeeldingsstap &#x200B;](/help/destinations/ui/last-qualification-time.gif) tonen

## Meer informatie {#more-information}

Voor uitgebreide informatie over het activeren van gegevens aan op dossier-gebaseerde bestemmingen met inbegrip van alle stappen in het werkschema en noodzakelijke toestemmingen, lees [&#x200B; op dossier-gebaseerde bestemmingsleerprogramma &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) activeren.
