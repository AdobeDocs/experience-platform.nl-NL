---
title: IP adres lijst van gewenste personen voor op dossier-gebaseerde cloudopslagbestemmingen
type: Documentation
description: Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform naar de bestemmingen van de wolkenopslag veilig uit te voeren.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: ee4c42a2298c588590b1535524ed8f3dfe13b603
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# IP adres lijst van gewenste personen voor op dossier-gebaseerde cloudopslagbestemmingen {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe raadt u aan deze pagina als bladwijzer te bekijken en deze elke drie maanden opnieuw te bekijken om te controleren op de meest recente IP-adressen. Adobe geeft geen melding van nieuwe IP-bereiken.
> * Hoewel Adobe gegevensexport naar SFTP-servers ondersteunt, zijn de aanbevolen locaties voor cloudopslag voor het exporteren van gegevens [!DNL Amazon S3] en [!DNL Azure Blob] .

## Toepasselijkheid {#applicability}

De informatie over het IP-bereik op deze pagina is van toepassing op de volgende op bestanden gebaseerde cloudopslagconnectors in de doelcatalogus:

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google Cloud Storage]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>De IP waaiers die op deze pagina worden gedocumenteerd worden ** niet gesteund voor de volgende op dossier-gebaseerde bestemmingen van de wolkenopslag: [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2] en [!UICONTROL Data Landing Zone].

## Overzicht {#overview}

Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform naar verscheidene bestemmingen van de wolkenopslag veilig uit te voeren.

U kunt besturingselementen voor netwerktoegang definiëren via uw netwerkfirewall. Door de aangewezen IP waaier te specificeren, kunt u verkeer voor de dienst van de gegevensoverdracht toestaan.

Adobe raadt u aan de volgende IP-bereiken aan een lijst van gewenste personen toe te voegen voordat u met de bestemmingsverbindingen voor cloudopslag werkt. Als u er niet in slaagt uw regiospecifieke IP-bereik aan uw lijst van gewenste personen toe te voegen, kan dit leiden tot fouten of niet-prestaties bij het gebruik van de bestemmingsverbindingen voor cloudopslag.

## Vereist voor alle klanten {#all-customers}

* `52.247.108.70`
<!-- 
## US customers running on AWS {#aws}

The IP range below applies to Experience Platform customers running on Amazon Web Services (AWS). See the [Experience Platform Multi-Cloud overview](../../../landing/multi-cloud.md) for more information.

>[!NOTE]
>
>This IP range is not supported for customers running on AWS who use file-based destinations to export data to Amazon S3. -->

* `66.117.18.0/24`

## Amerikaanse klanten {#us-customers}

* `52.252.71.64/29`

## Canada-klanten {#canada-customers}

* `20.220.135.16/29`

## EMEA-klanten {#emea-customers}

* `51.137.8.208/29`

## Britse klanten {#uk-customers}

* `20.26.133.96/29`

## APAC-klanten {#apac-customers}

* `20.53.201.168/29`
