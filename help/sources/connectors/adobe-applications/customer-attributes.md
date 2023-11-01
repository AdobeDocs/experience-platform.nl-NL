---
keywords: Experience Platform;thuis;populaire onderwerpen;Klantenkenmerk-aansluiting
solution: Experience Platform
title: Overzicht van de Source Connector voor klantkenmerken
description: Leer hoe u klantkenmerken met behulp van API's of de gebruikersinterface kunt verbinden met Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Klantenkenmerkaansluiting

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html) in Experience Cloud laat u toe om uw gevangen ondernemingsgegevens van een gegevensbestand van het het relatiebeheer van de klant (CRM) te uploaden. U kunt de gegevens uploaden naar een gegevensbron voor klantkenmerken in het Experience Cloud en vervolgens de gegevens in Adobe Analytics en Adobe Target gebruiken.

Experience Platform biedt ondersteuning voor opnemen [!DNL Customer Attributes] profielgegevens naar Adobe Experience Platform.

## Gegevenssets en schema&#39;s

De [!DNL Customer Attributes] De bron leidt automatisch tot de dataset voor gegevens om in te landen. Deze automatisch gemaakte gegevensset is vast en kan niet handmatig worden geselecteerd. De bron leidt ook auto-creeert het schema voor de dataset die op de inputgegevensbron wordt gebaseerd. Dit proces impliceert ook de auto-creatie van de noodzakelijke afbeeldingen tussen het schema en de brongegevens.

## Identiteiten

De primaire identiteit van een dataset is bevat in de eerste kolom van het Csv- dossier van de brongegevens. De [!DNL Customer Attributes] de bron veronderstelt dat de identiteit altijd aan in kaart wordt gebracht [`CORE` namespace](../../../identity-service/namespaces.md), een door het systeem gegenereerde naamruimte die door [[!DNL Identity Service]](../../../identity-service/home.md).

U kunt geen bestaande naamruimte voor de identiteit selecteren wanneer u [!DNL Customer Attributes] bron omdat [!DNL Customer Attributes] veronderstelt dat de primaire identiteit voor het schema altijd in de identiteitskaart is. [!DNL Customer Attributes] maakt vervolgens op geautomatiseerde wijze de toewijzing van de bron-id aan de UUID van de identiteitskaart.

Voor [!DNL Customer Attributes] gegevens die aan andere [!DNL Profile] gegevenssets, de gegevens en identiteiten ervan moeten kunnen worden gekoppeld aan een Experience Cloud-id.

U kunt de `CORE` naamruimte door de Experience Cloud-id voor de bezoeker in te stellen met [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/)of de [API voor Experience Cloud-id](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html).

De [!DNL Customer Attributes] andere identiteitsrelaties niet meer vullen. Als een [!DNL Customer Attributes] brondataset bevat een **E-mail** en **Loyalty-id** veld, moeten deze velden worden gelabeld als identiteitsvelden in het schema om te kunnen worden verwerkt tot [!DNL Identity Service].

Zie de zelfstudie aan [een [!DNL Customer Attributes] bronverbinding in de gebruikersinterface](../../tutorials/ui/create/adobe-applications/customer-attributes.md) voor meer informatie .
