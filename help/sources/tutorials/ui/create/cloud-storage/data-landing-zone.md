---
keywords: Experience Platform;thuis;populaire onderwerpen;Data Landing Zone;data landingszone
solution: Experience Platform
title: Gegevenslandingszone verbinden met Platform via de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe te om een van de Bron van de Gebied van Gegevens te creëren die de gebruikersinterface van het Platform gebruiken.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# [!DNL Data Landing Zone] verbinden met Platform gebruikend UI

[!DNL Data Landing Zone] is een op cloud gebaseerde gegevensopslagfaciliteit voor tijdelijke opslag van bestanden die bij Adobe Experience Platform wordt geleverd. [!DNL Data Landing Zone] wordt alleen gebruikt voor het in- en uitstappen van gegevens in en uit het Platform. Gegevens worden na zeven dagen automatisch verwijderd uit [!DNL Data Landing Zone].

Deze zelfstudie bevat stappen voor het maken van een [!DNL Data Landing Zone]-bronverbinding met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Breng uw bestanden van [!DNL Data Landing Zone] naar Platform

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Platform in de linkernavigatie om de werkruimte [!UICONTROL Sources] te openen. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer [!UICONTROL cloud storage] onder de categorie [!DNL Data Landing Zone] en selecteer **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/dlz/catalog.png)

De stap [!UICONTROL Add data] verschijnt, die u van een interface voorzien om de gegevens te selecteren en voor te proef u aan Platform wilt brengen.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

Voor een gedetailleerde, geleidelijke gids over hoe te om een gegevensstroom voor een bron van de wolkenopslag tot stand te brengen, zie de zelfstudie op [het creëren van een gegevensstroom van de wolkenopslag om gegevens aan Platform](../../dataflow/batch/cloud-storage.md) te brengen.

## Uw [!DNL Data Landing Zone]-referenties ophalen en vernieuwen

[!DNL Data Landing Zone] is een out-of-the-box bron die wordt geleverd bij uw Adobe Experience Platform Sources-licentie. [!DNL Data Landing Zone] gebruikt een SAS URI- en SAS-tokenverificatie. U kunt uw verificatiegegevens ophalen en vernieuwen op de pagina [!UICONTROL Sources catalog].

Selecteer in [!UICONTROL Sources catalog] onder de categorie [!UICONTROL Cloud storage] de ellipsen (**..**) van de **[!UICONTROL Data Landing Zone]**-kaart. Selecteer **[!UICONTROL View credentials]** in het vervolgkeuzemenu dat wordt weergegeven.

![opties](../../../../images/tutorials/create/dlz/options.png)

Er wordt een pop-up weergegeven met uw containernaam, SAS-token, naam van opslagaccount en SAS-URI.

Selecteer **[!UICONTROL Refresh credentials]** en wacht een paar seconden tot uw bijgewerkte referenties worden verwerkt.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u tot uw [!DNL Data Landing Zone] container toegang en geleerd om uw geloofsbrieven terug te winnen en te verfrissen. U kunt nu verdergaan naar de volgende zelfstudie op [het maken van een gegevensstroom om gegevens van een cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
