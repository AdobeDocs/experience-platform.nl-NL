---
keywords: IP adres, IP waaier, de bestemmingen van de lijst van gewenste personen, de lijst van gewenste personen, lijst van gewenste personen die bestemmingen stromen
title: IP adres lijst van gewenste personen voor het stromen bestemmingen
type: Documentation
description: Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform veilig naar uw eindpunt van HTTP REST API, Amazon Kinesis, of de instantie van de Hubs van de Gebeurtenis te uitvoeren Azure.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 118b0b5e6a1936b644da4153fe7bfeb872ae137e
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# IP adres lijst van gewenste personen voor het stromen bestemmingen {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe raadt u aan deze pagina als bladwijzer te bekijken en deze elke drie maanden opnieuw te bekijken om te controleren op de meest recente IP-adressen. Adobe geeft geen melding van nieuwe IP-bereiken.
> * De lijst van hier gedocumenteerde IPs *is niet* op om het even welke bestemmingen van toepassing u gebruikend [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md) bouwt.

## Overzicht {#overview}

De hier gedocumenteerde IP waaiers zijn op de volgende bestemmingen van toepassing:

* [HTTP API-bestemming](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Het uitgaande verkeer van Experience Platform aan deze bestemmingen gaat altijd door IPs op deze pagina wordt vermeld die.

Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform naar uw eindpunt van HTTP veilig uit te voeren, [!DNL Amazon Kinesis], of [!DNL Azure Event Hubs] instantie. Deze functionaliteit is vooral nuttig als uw eindpunt van HTTP achter een ondernemingsfirewall wordt gevestigd of als uw bedrijfveiligheid en nalevingsnormen een lijst van IP waaiers vereisen om worden gevoegd op lijst van gewenste personen.

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
`20.22.83.112`

## VA6: Amerikaanse en Amerikaanse klanten die op AWS rijden {#aws}

Het onderstaande IP-bereik is van toepassing op Experience Platform-klanten die op Amazon Web Services (AWS) draaien. Zie het [ overzicht van de Multi-Cloud van Experience Platform ](../../../landing/multi-cloud.md) voor meer informatie.

`66.117.18.0/24`

## NLD2: EMEA-klanten {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`20.101.246.9`
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
`20.101.233.128`

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
`20.53.206.128`
`20.227.35.177`

## CAN2: klanten uit Canada {#can}

`20.104.46.128/28`
`20.104.46.160/28`
`20.104.46.64/28`
`20.104.46.80/28`
`20.116.145.94`
`20.116.147.168`
`20.200.70.192/28`
`20.200.70.208/28`
`20.200.70.224/28`
`20.200.70.240/28`
`20.200.71.0/28`
`20.200.71.112/28`
`20.200.71.128/28`
`20.200.71.144/28`
`20.200.71.16/28`
`20.200.71.160/28`
`20.200.71.176/28`
`20.200.71.32/28`
`20.200.71.48/28`
`20.200.71.64/28`
`20.200.71.80/28`
`20.200.71.96/28`
`20.200.93.180`
`20.200.94.116`
`20.200.94.83`

## GBR9: klanten in Groot-Brittannië {#gbr}

`20.254.3.48/28`
`20.254.4.0/28`
`20.26.128.247`
`20.254.1.128/28`
`20.254.2.32/28`
`20.26.64.208/28`
`20.254.2.208/28`
`20.254.3.176/28`
`20.254.4.64/28`
`20.254.3.32/28`
`20.254.3.144/28`
`20.26.64.240/28`
`20.254.4.16/28`
`20.254.3.240/28`
`20.26.65.0/28`
`20.254.4.32/28`
`20.254.3.112/28`
`20.254.4.96/28`
`20.108.202.84`
`20.108.119.100`
`20.254.2.128/28`
`20.26.131.71`
`20.26.130.226`
`20.26.64.112/28`
`20.254.3.192/28`