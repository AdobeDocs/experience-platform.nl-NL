---
title: Amazon S3-bestemming
seo-title: Amazon S3-bestemming
description: Maak een live uitgaande verbinding met uw Amazon Web Services (AWS) S3-opslag om periodiek door tabs gescheiden of CSV-gegevensbestanden van het Adobe Experience Platform naar uw eigen S3-emmers te exporteren.
seo-description: Maak een live uitgaande verbinding met uw Amazon Web Services (AWS) S3-opslag om periodiek door tabs gescheiden of CSV-gegevensbestanden van het Adobe Experience Platform naar uw eigen S3-emmers te exporteren.
translation-type: tm+mt
source-git-commit: acd3865be4994a478048d317060c55b7e0d9914c

---


# Amazon S3-bestemming

## Overzicht

Maak een live uitgaande verbinding met uw Amazon Web Services (AWS) S3-opslag om periodiek door tabs gescheiden of CSV-gegevensbestanden van het Adobe Experience Platform naar uw eigen S3-emmers te exporteren.

## Connect-doel {#connect-destination}

Zie de workflow voor [Cloud-opslagdoelen ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)voor instructies over hoe u verbinding kunt maken met uw cloudopslagdoelen, waaronder Amazon S3.

Voor Amazon S3 bestemmingen, ga de volgende informatie in tot bestemmingswerkschema:

* **Amazon S3-toegangstoets en Amazon S3-geheime sleutel**: In Amazon S3, produceer een toegangstoets - geheim toegangszeer belangrijk paar om Adobe in real time CDP toegang tot uw Amazon S3 rekening te verlenen;
* **Amazon S3-pad**: Dit is de locatie in uw Amazon S3-emmertje waar Adobe Real-time CDP exportbestanden levert.


>[!IMPORTANT]
>
>Adobe Real-time CDP heeft `write` machtigingen nodig voor het emmerobject waar de exportbestanden worden geleverd.
