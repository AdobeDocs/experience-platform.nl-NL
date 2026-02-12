---
keywords: IP adres, IP waaier, de bestemmingen van de lijst van gewenste personen, de lijst van gewenste personen, lijst van gewenste personen die bestemmingen stromen
title: IP adres lijst van gewenste personen voor het stromen bestemmingen
type: Documentation
description: Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform veilig naar uw HTTP REST API eindpunt, of de instantie van Amazon te exporteren Kinesis.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 6d59d0555dda124acfd16483e11c2899ff5c846e
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---


# IP adres lijst van gewenste personen voor het stromen API-Gebaseerde bestemmingen {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe raadt u aan deze pagina als bladwijzer te bekijken en deze elke drie maanden opnieuw te bekijken om te controleren op de meest recente IP-adressen. Adobe geeft geen melding van nieuwe IP-bereiken.

## Overzicht {#overview}

De IP waaiers die in deze pagina worden gedocumenteerd zijn op de volgende bestemmingen van toepassing:

* [&#x200B; Geavanceerde ondernemingsbestemmingen &#x200B;](../../destination-types.md#advanced-enterprise-destinations): [&#x200B; HTTP API bestemming &#x200B;](./http-destination.md), en [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [&#x200B; het stromen publiek de uitvoerbestemmingen van de publiek &#x200B;](../../destination-types.md#streaming-destinations), zoals [&#x200B; PegCDH Realtime Publiek &#x200B;](/help/destinations/catalog/personalization/pega-v2.md), op API-Gebaseerde integratie met [&#x200B; Salesforce Marketing Cloud &#x200B;](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) en [&#x200B; Oracle Eloqua &#x200B;](/help/destinations/catalog/email-marketing/oracle-eloqua-api.md)
* Openbare of privébestemmingen die via [Destination SDK](../../destination-sdk/getting-started.md) zijn opgebouwd

>[!IMPORTANT]
>
>De IP waaiers die op deze pagina worden gedocumenteerd zijn *niet* gesteund voor [!DNL Azure Event Hubs] bestemmingen en het stromen op API-Gebaseerde bestemmingen die op Microsoft Azure worden ontvangen.


Het uitgaande verkeer van Experience Platform aan deze bestemmingen gaat altijd door IPs op deze pagina wordt vermeld die.

Deze pagina verstrekt IP waaiers die u aan uw lijst van gewenste personen kunt toevoegen, om gegevens van Experience Platform naar de hierboven vermelde bestemmingen veilig uit te voeren. Deze functionaliteit is vooral nuttig als uw eindpunt van HTTP achter een ondernemingsfirewall wordt gevestigd of als uw bedrijfveiligheid en nalevingsnormen een lijst van IP waaiers vereisen om worden gevoegd op lijst van gewenste personen.

U kunt besturingselementen voor netwerktoegang definiëren via uw netwerkfirewall. Door de aangewezen IP waaier te specificeren, kunt u verkeer voor de dienst van de gegevensoverdracht toestaan.

## Wanneer om IPs in deze pagina te lijsten van gewenste personen {#when-to-allowlist}

Als uw organisatiebeleid u vereist om IPs voor inkomend verkeer te lijsten van gewenste personen, moet u de IP waaiers van de volgende categorieën aan uw lijst van gewenste personen toevoegen voorafgaand aan het werken met de hierboven vermelde bestemmingen op deze pagina:

1. Alle [&#x200B; globale IP adressen &#x200B;](#global)
2. Naast de globale IP adressen, voeg de IP adressen toe die aan het gebied beantwoorden u binnen, van de lijst verder onderaan de pagina wordt voorzien. Als u er niet in slaagt om uw regiospecifieke IP-bereik aan uw lijst van gewenste personen toe te voegen, kan dit leiden tot fouten of niet-prestaties bij het gebruik van deze streamingdoelen.

## Algemene IP-adressen {#global}

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

Naast deze globale IP adressen, moet u de IP adressen voor het gebied lijsten van gewenste personen waar uw organisatie van de lijst hieronder wordt voorzien.

## VA7: Amerikaanse en Amerikaanse klanten {#us-americas}

* `4.152.211.251`
* `20.22.83.112`
* `20.186.185.181`
* `20.186.185.227`
* `20.186.185.239`
* `40.70.154.136/29`
* `52.254.105.192/28`
* `52.254.106.0/28`
* `52.254.106.144/28`
* `52.254.106.160/28`
* `52.254.106.176/28`
* `52.254.106.192/28`
* `52.254.106.208/28`
* `52.254.106.224/28`
* `52.254.106.240/28`
* `52.254.107.0/28`
* `52.254.107.16/28`
* `52.254.107.32/28`
* `52.254.107.64/28`
* `52.254.107.80/28`
* `52.254.107.128/28`
* `52.254.107.144/28`

## VA6: Amerikaanse en Amerikaanse klanten die op AWS rijden {#aws}

Het onderstaande IP-bereik is van toepassing op Experience Platform-klanten die op Amazon Web Services (AWS) draaien. Zie het [&#x200B; overzicht van de Multi-Cloud van Experience Platform &#x200B;](../../../landing/multi-cloud.md) voor meer informatie.

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

## NLD2: EMEA-klanten {#emea}

* `20.50.23.153`
* `20.101.246.9`
* `40.74.3.176/28`
* `40.74.4.144/28`
* `40.74.4.160/28`
* `40.74.4.176/28`
* `40.74.5.128/28`
* `40.74.6.80/28`
* `40.74.6.96/28`
* `40.74.6.112/28`
* `40.74.6.128/28`
* `40.74.6.144/28`
* `40.74.7.128/28`
* `40.74.7.144/28`
* `40.74.7.160/28`
* `40.74.7.176/28`
* `40.74.7.192/28`
* `40.74.7.208/28`
* `51.105.144.1`
* `51.105.144.81`
* `51.124.70.4`
* `51.144.184.248/29`
* `52.142.236.87`
* `108.141.12.47`

## AUS5: APAC-klanten {#apac}

* `20.40.188.166`
* `20.40.188.194`
* `20.40.188.227`
* `20.40.191.96/28`
* `20.40.191.224/28`
* `20.40.191.240/28`
* `20.43.104.0/28`
* `20.43.104.16/28`
* `20.43.104.32/28`
* `20.43.104.48/28`
* `20.43.104.64/28`
* `20.43.104.80/28`
* `20.43.104.96/28`
* `20.43.104.112/28`
* `20.43.104.128/28`
* `20.43.104.144/28`
* `20.43.104.160/28`
* `20.43.104.176/28`
* `20.43.104.192/28`
* `20.43.105.0/28`
* `20.43.105.16/28`
* `20.43.105.32/28`
* `20.43.105.48/28`
* `20.227.35.177`
* `20.53.206.128`

## CAN2: klanten uit Canada {#can}

* `20.104.46.64/28`
* `20.104.46.80/28`
* `20.104.46.128/28`
* `20.104.46.160/28`
* `20.116.145.94`
* `20.116.147.168`
* `20.200.70.192/28`
* `20.200.70.208/28`
* `20.200.70.224/28`
* `20.200.70.240/28`
* `20.200.71.0/28`
* `20.200.71.16/28`
* `20.200.71.32/28`
* `20.200.71.48/28`
* `20.200.71.64/28`
* `20.200.71.80/28`
* `20.200.71.96/28`
* `20.200.71.112/28`
* `20.200.71.128/28`
* `20.200.71.144/28`
* `20.200.71.160/28`
* `20.200.71.176/28`
* `20.200.93.180`
* `20.200.94.83`
* `20.200.94.116`

## GBR9: klanten in Groot-Brittannië {#gbr}

* `20.26.64.112/28`
* `20.26.64.208/28`
* `20.26.64.240/28`
* `20.26.65.0/28`
* `20.26.128.247`
* `20.26.130.226`
* `20.26.131.71`
* `20.108.119.100`
* `20.108.202.84`
* `20.254.1.128/28`
* `20.254.2.32/28`
* `20.254.2.128/28`
* `20.254.2.208/28`
* `20.254.3.32/28`
* `20.254.3.48/28`
* `20.254.3.112/28`
* `20.254.3.144/28`
* `20.254.3.176/28`
* `20.254.3.192/28`
* `20.254.3.240/28`
* `20.254.4.0/28`
* `20.254.4.16/28`
* `20.254.4.32/28`
* `20.254.4.64/28`
* `20.254.4.96/28`

## IND2: Indiase klanten {#india}

* `4.188.4.11`
* `4.188.4.99`
* `4.188.4.138`
* `4.188.4.154`
* `4.188.4.167`
* `4.213.40.145`
* `4.224.74.0/28`
* `4.224.74.64/28`
* `4.224.74.80/28`
* `4.224.74.96/28`
* `20.244.74.112/28`
* `20.244.77.0/28`
* `20.244.77.16/28`
* `20.244.77.160/28`
* `20.244.77.208/28`
* `20.244.78.0/28`
* `20.244.78.208/28`
* `20.244.79.0/28`
* `20.244.79.16/28`
* `20.244.79.48/28`
* `20.244.79.80/28`
* `20.244.79.128/28`
* `20.244.79.144/28`
* `20.244.79.192/28`
* `20.244.79.208/28`
* `20.244.79.224/28`

