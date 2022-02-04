---
keywords: Experience Platform;thuis;populaire onderwerpen;Data Landing Zone;data landingszone
solution: Experience Platform
title: Gegevenslandingszone verbinden met Platform via de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe te om een van de Bron van de Gebied van Gegevens te creëren die de gebruikersinterface van het Platform gebruiken.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: b007cdf92811b453df5b5d005456a05cd845b769
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Verbinden [!DNL Data Landing Zone] naar Platform met behulp van de gebruikersinterface

[!DNL Data Landing Zone] is een op cloud gebaseerde gegevensopslagfaciliteit voor tijdelijke opslag van bestanden die bij Adobe Experience Platform wordt geleverd. Gegevens worden automatisch verwijderd uit de [!DNL Data Landing Zone] na zeven dagen.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Data Landing Zone] bronverbinding via de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Bestanden ophalen van [!DNL Data Landing Zone] naar Platform

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL cloud storage] categorie, selecteert u [!DNL Data Landing Zone] en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/dlz/catalog.png)

De [!UICONTROL Add data] wordt weergegeven, zodat u een interface hebt voor het selecteren en voorvertonen van de gegevens die u naar het Platform wilt verzenden.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

Raadpleeg de zelfstudie voor een gedetailleerde, stapsgewijze handleiding voor het maken van een gegevensstroom voor een bron voor cloudopslag. [een gegevensstroom voor cloudopslag maken om gegevens naar het Platform te brengen](../../dataflow/batch/cloud-storage.md).

## Ophalen en vernieuwen uw [!DNL Data Landing Zone] geloofsbrieven

[!DNL Data Landing Zone] is een out-of-the-box bron die wordt geleverd bij uw Adobe Experience Platform Sources-licentie. [!DNL Data Landing Zone] gebruikt een SAS URI- en SAS-tokenverificatie. U kunt uw verificatiegegevens ophalen en vernieuwen via het dialoogvenster [!UICONTROL Sources catalog] pagina.

In de [!UICONTROL Sources catalog], onder de [!UICONTROL Cloud storage] categorie, selecteer de ellipsen (**...**) van de **[!UICONTROL Data Landing Zone]** kaart. Selecteer in het vervolgkeuzemenu dat wordt weergegeven de optie **[!UICONTROL View credentials]**.

![opties](../../../../images/tutorials/create/dlz/options.png)

Er wordt een pop-up weergegeven met uw containernaam, SAS-token, naam van opslagaccount en SAS-URI.

Selecteren **[!UICONTROL Refresh credentials]** en kan het enkele seconden duren voordat uw bijgewerkte referenties worden verwerkt.

>[!TIP]
>
>Uw [!DNL Data Landing Zone] gebruikersgegevens verlopen automatisch na 90 dagen en u moet nieuwe gegevens gebruiken om opnieuw verbinding te maken met [!DNL Data Landing Zone] na afloop. Uw gegevensstromen in Platform worden niet beïnvloed door het verlopen van geloofsbrieven en u kunt nog met nieuwe en bestaande gegevensstromen met uw nieuwe geloofsbrieven blijven werken.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Volgende stappen

Door deze zelfstudie te volgen hebt u toegang tot uw [!DNL Data Landing Zone] en geleerd om uw geloofsbrieven terug te winnen en te verfrissen. U kunt nu verdergaan met de volgende zelfstudie [een gegevensstroom maken om gegevens van een cloudopslag naar het Platform te brengen](../../dataflow/batch/cloud-storage.md).
