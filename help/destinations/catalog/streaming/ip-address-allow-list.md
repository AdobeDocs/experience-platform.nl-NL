---
keywords: IP adres, IP waaier, de bestemmingen van de lijst van gewenste personen, de lijst van gewenste personen, lijst van gewenste personen die bestemmingen stromen
title: 'IP adres lijst van gewenste personen voor het stromen bestemmingen '
type: Documentation
description: Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform naar uw HTTP REST API eindpunt veilig uit te voeren.
source-git-commit: 508435ebe7ba762d204408118703fa6469616118
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# IP adres lijst van gewenste personen voor het stromen bestemmingen {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe raadt u aan een bladwijzer op deze pagina te maken en deze elke drie maanden opnieuw te bekijken om te controleren op de meest recente IP-adressen. Adobe verstrekt geen bericht van nieuwe IP waaiers.
> * De lijst van hier gedocumenteerde IPs *niet* is van toepassing op om het even welke bestemmingen u gebruikend bouwt [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).


## Overzicht {#overview}

De hier gedocumenteerde IP waaiers zijn op de volgende bestemmingen van toepassing:

* [HTTP API-bestemming](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Het uitgaande verkeer van Experience Platform aan deze bestemmingen gaat altijd door IPs op deze pagina wordt vermeld die.

Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform aan uw eindpunt van HTTP veilig uit te voeren, [!DNL Amazon Kinesis], of [!DNL Azure Event Hubs] -instantie. Deze functionaliteit is vooral nuttig als uw eindpunt van HTTP achter een ondernemingsfirewall wordt gevestigd of als uw bedrijfveiligheid en nalevingsnormen een lijst van IP waaiers vereisen om worden gevoegd op lijst van gewenste personen.

U kunt besturingselementen voor netwerktoegang definiëren via uw netwerkfirewall. Door de aangewezen IP waaier te specificeren, kunt u verkeer voor de dienst van de gegevensoverdracht toestaan.

Adobe adviseert dat u de volgende IP waaiers aan een lijst van gewenste personen voorafgaand aan het werken met de hierboven vermelde bestemmingen op deze pagina toevoegt. Als u er niet in slaagt om uw regiospecifieke IP-bereik aan uw lijst van gewenste personen toe te voegen, kan dit leiden tot fouten of niet-prestaties bij het gebruik van deze streamingdoelen.

## VA7: Amerikaanse en Amerikaanse klanten {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`

## NLD2: EMEA-klanten {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`

## AUS5: APAC-klanten {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`