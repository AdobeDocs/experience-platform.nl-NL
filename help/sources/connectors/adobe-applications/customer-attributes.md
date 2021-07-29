---
keywords: Experience Platform;thuis;populaire onderwerpen;Klantenkenmerk-aansluiting
solution: Experience Platform
title: Overzicht van de Source Connector voor klantkenmerken
topic-legacy: overview
description: Leer hoe u klantkenmerken met behulp van API's of de gebruikersinterface kunt verbinden met Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Customer Attributes-connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) in Experience Cloud kunt u uw vastgelegde bedrijfsgegevens uploaden vanuit een CRM-database (Customer relationship management). U kunt de gegevens uploaden naar een gegevensbron voor klantkenmerken in de Experience Cloud en vervolgens de gegevens in Adobe Analytics en Adobe Target gebruiken.

Experience Platform biedt ondersteuning voor het opnemen van [!DNL Customer Attributes]-profielgegevens in Adobe Experience Platform.

## Gegevenssets en schema&#39;s

De bron [!DNL Customer Attributes] leidt automatisch tot de dataset voor gegevens om in te landen. Deze automatisch gemaakte gegevensset is vast en kan niet handmatig worden geselecteerd. De bron leidt ook auto-creeert het schema voor de dataset die op de inputgegevensbron wordt gebaseerd. Dit proces impliceert ook de auto-creatie van de noodzakelijke afbeeldingen tussen het schema en de brongegevens.

## Identiteiten

De primaire identiteit van een dataset is bevat in de eerste kolom van het Csv- dossier van de brongegevens. De [!DNL Customer Attributes] bron veronderstelt dat de identiteit altijd aan [`CORE` namespace](../../../identity-service/namespaces.md), een systeem-geproduceerde namespace in kaart wordt gebracht die door [[!DNL Identity Service]](../../../identity-service/home.md) wordt gesteund.

U kunt geen bestaande namespace voor de identiteit selecteren wanneer het gebruiken van [!DNL Customer Attributes] bron omdat [!DNL Customer Attributes] veronderstelt dat de primaire identiteit voor het schema altijd in de identiteitskaart is. [!DNL Customer Attributes] maakt vervolgens op geautomatiseerde wijze de toewijzing van de bron-id aan de UUID van de identiteitskaart.

Gegevens [!DNL Customer Attributes] kunnen alleen worden gekoppeld aan andere [!DNL Profile]-gegevenssets als de gegevens en identiteiten ervan kunnen worden gekoppeld aan een Experience Cloud-id.

U kunt de naamruimte `CORE` instellen door de Experience Cloud-id voor de bezoeker in te stellen met [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity) of [Experience Cloud ID Service API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

In het [!DNL Customer Attributes]-bestand worden geen andere identiteitsrelaties meer ingevuld. Als een [!DNL Customer Attributes] brondataset bijvoorbeeld een **Email** en een **Loyalty ID** gebied bevat, dan moeten die gebieden als identiteitsgebieden in het schema worden geëtiketteerd om tot [!DNL Identity Service] te worden verwerkt.

Zie de zelfstudie op [het creëren van a [!DNL Customer Attributes] bronverbinding in UI](../../tutorials/ui/create/adobe-applications/customer-attributes.md) voor meer informatie.
