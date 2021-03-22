---
keywords: IP adres, IP waaier, de bestemmingen van de lijst van gewenste personen
title: 'IP adres lijst van gewenste personen voor wolkenopslagbestemmingen '
type: Documentatie
description: Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform aan uw server SFTP, Amazon S3, of opslag van Azure Blob veilig uit te voeren.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# IP adres lijst van gewenste personen voor wolkenopslagbestemmingen {#ip-address-allow-list}

## Overzicht {#overview}

>[!IMPORTANT]
>
> Adobe raadt u aan een bladwijzer op deze pagina te maken en deze elke drie maanden opnieuw te bekijken om te controleren op de meest recente IP-adressen. Adobe verstrekt geen bericht van nieuwe IP waaiers.

Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform aan uw [SFTP server ](./sftp.md), [Amazon S3](./amazon-s3.md), of [Azure Blob](./azure-blob.md) opslag veilig uit te voeren.

U kunt besturingselementen voor netwerktoegang definiëren via uw netwerkfirewall. Door de aangewezen IP waaier te specificeren, kunt u verkeer voor de dienst van de gegevensoverdracht toestaan.

U kunt de volgende IP waaiers aan een lijst van gewenste personen toevoegen alvorens met de bestemmingsverbindingen van de wolkenopslag te werken. Als u het regiospecifieke IP-bereik niet aan uw lijst van gewenste personen toevoegt, kan dit leiden tot fouten of tot niet-prestaties bij het gebruik van de bestemmingsverbindingen voor cloudopslag.

## Amerikaanse klanten

* `52.252.71.64/29`

## EMEA-klanten

* `51.137.8.208/29`

## APAC-klanten

* `20.53.201.168/29`