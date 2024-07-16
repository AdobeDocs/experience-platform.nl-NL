---
keywords: Experience Platform;thuis;populaire onderwerpen;Klantenkenmerk-aansluiting
solution: Experience Platform
title: Customer Attributes Source Connector Overview
description: Leer hoe u klantkenmerken met behulp van API's of de gebruikersinterface kunt verbinden met Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Klantenkenmerkaansluiting

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

[[!DNL Customer Attributes] ](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html) in Experience Cloud laat u toe om uw gevangen ondernemingsgegevens van een gegevensbestand van het beheer van de klantenverhouding (CRM) te uploaden. U kunt de gegevens uploaden naar een gegevensbron voor klantkenmerken in het Experience Cloud en vervolgens de gegevens in Adobe Analytics en Adobe Target gebruiken.

Experience Platform biedt ondersteuning voor het opnemen van [!DNL Customer Attributes] -profielgegevens in Adobe Experience Platform.

## Gegevenssets en schema&#39;s

De [!DNL Customer Attributes] -bron maakt automatisch de gegevensset waarin gegevens moeten worden geland. Deze automatisch gemaakte gegevensset is vast en kan niet handmatig worden geselecteerd. De bron leidt ook auto-creeert het schema voor de dataset die op de inputgegevensbron wordt gebaseerd. Dit proces impliceert ook de auto-creatie van de noodzakelijke afbeeldingen tussen het schema en de brongegevens.

## Identiteiten

De primaire identiteit van een dataset is bevat in de eerste kolom van het Csv- dossier van de brongegevens. De [!DNL Customer Attributes] bron veronderstelt dat de identiteit altijd aan [`CORE` namespace ](../../../identity-service/features/namespaces.md) wordt in kaart gebracht, een systeem-geproduceerde namespace die door [[!DNL Identity Service]](../../../identity-service/home.md) wordt gesteund.

U kunt bij het gebruik van [!DNL Customer Attributes] source geen bestaande naamruimte voor de identiteit selecteren omdat [!DNL Customer Attributes] ervan uitgaat dat de primaire identiteit voor het schema altijd in de identiteitskaart staat. [!DNL Customer Attributes] maakt vervolgens op geautomatiseerde wijze de toewijzing van de bron-id aan de UUID van de identiteitskaart.

[!DNL Customer Attributes] -gegevens kunnen alleen worden gekoppeld aan andere [!DNL Profile] -gegevenssets als de gegevens en identiteiten ervan kunnen worden gekoppeld aan een Experience Cloud-id.

U kunt `CORE` namespace vestigen door Experience Cloud identiteitskaart voor de bezoeker te plaatsen die [ Web SDK ](/help/web-sdk/identity/overview.md), [ Mobiele SDK ](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/), of [ de Dienst API van identiteitskaart van het Experience Cloud ](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) gebruikt.

In het bestand [!DNL Customer Attributes] worden andere identiteitsrelaties niet meer ingevuld. Bijvoorbeeld, als a [!DNL Customer Attributes] brondataset een **E-mail** en gebied van identiteitskaart van de a **Loyalty** bevat, dan moeten die gebieden als identiteitsgebieden in het schema worden geëtiketteerd om in [!DNL Identity Service] te worden verwerkt.

Zie het leerprogramma op [ creërend a  [!DNL Customer Attributes]  bronverbinding in UI ](../../tutorials/ui/create/adobe-applications/customer-attributes.md) voor meer informatie.
