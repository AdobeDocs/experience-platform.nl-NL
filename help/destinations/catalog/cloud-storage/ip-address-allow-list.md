---
keywords: IP adres, IP waaier, de bestemmingen van de lijst van gewenste personen, de lijst van gewenste personen
title: 'IP adres lijst van gewenste personen voor wolkenopslagbestemmingen '
type: Documentation
description: Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform aan uw server SFTP, Amazon S3, of opslag van Azure Blob veilig uit te voeren.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: 4cc7fb2714f6df8065a0531f7e507983940d662c
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# IP adres lijst van gewenste personen voor wolkenopslagbestemmingen {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe raadt u aan een bladwijzer op deze pagina te maken en deze elke drie maanden opnieuw te bekijken om te controleren op de meest recente IP-adressen. Adobe verstrekt geen bericht van nieuwe IP waaiers.
> * Hoewel Adobe gegevensuitvoer naar SFTP-servers ondersteunt, zijn de aanbevolen locaties voor cloudopslag voor het exporteren van gegevens [!DNL Amazon S3] en [!DNL Azure Blob].


## Overzicht {#overview}

Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform aan uw [server SFTP veilig uit te voeren ](./sftp.md).

U kunt besturingselementen voor netwerktoegang definiëren via uw netwerkfirewall. Door de aangewezen IP waaier te specificeren, kunt u verkeer voor de dienst van de gegevensoverdracht toestaan.

Adobe raadt u aan de volgende IP-bereiken toe te voegen aan een lijst van gewenste personen voordat u gaat werken met bestemmingsverbindingen voor cloudopslag. Als u het regiospecifieke IP-bereik niet aan uw lijst van gewenste personen toevoegt, kan dit leiden tot fouten of tot niet-prestaties bij het gebruik van de bestemmingsverbindingen voor cloudopslag.

## Vereist voor alle klanten

* `52.247.108.70`

## Amerikaanse klanten

* `52.252.71.64/29`

## EMEA-klanten

* `51.137.8.208/29`

## APAC-klanten

* `20.53.201.168/29`
