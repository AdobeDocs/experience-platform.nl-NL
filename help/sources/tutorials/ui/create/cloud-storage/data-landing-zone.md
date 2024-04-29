---
keywords: Experience Platform;thuis;populaire onderwerpen;Data Landing Zone;data landingszone
title: Gegevenslandingszone verbinden met platform via de gebruikersinterface
description: Leer hoe te om een van de Bron van de Gebied van Gegevens te creëren die de gebruikersinterface van het Platform gebruiken.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 9372e6f961015c989bfcb0d1e2b0129da965c522
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Verbinden [!DNL Data Landing Zone] naar Platform met behulp van UI

>[!IMPORTANT]
>
>Deze pagina is specifiek voor de [!DNL Data Landing Zone] *bron* in Experience Platform. Voor informatie over het verbinden met [!DNL Data Landing Zone] *doel* -aansluiting, verwijzen naar de [[!DNL Data Landing Zone] doeldocumentatiepagina](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] is een veilige, op de cloud gebaseerde opslagfaciliteit voor bestanden die naar Adobe Experience Platform kunnen worden overgebracht. Gegevens worden automatisch verwijderd uit het dialoogvenster [!DNL Data Landing Zone] na zeven dagen.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Data Landing Zone] bronverbinding via de gebruikersinterface van Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Bestanden ophalen van [!DNL Data Landing Zone] naar platform

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL cloud storage] categorie, selecteert u [!DNL Data Landing Zone] en selecteer vervolgens **[!UICONTROL Add data]**.

![De broncatalogus met de geselecteerde gegevenslandingszone.](../../../../images/tutorials/create/dlz/catalog.png)

De [!UICONTROL Add data] wordt weergegeven, zodat u een interface hebt voor het selecteren en voorvertonen van de gegevens die u naar het platform wilt verzenden.

* Het linkerdeel van de interface is een omslagbrowser, die u van een lijst van dossiers van uw container voorziet die u dan aan Platform kunt brengen.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een compatibel bestand voorvertonen.

Selecteer het bestand dat u naar het Experience Platform wilt brengen en wacht een paar minuten totdat de rechterinterface wordt bijgewerkt in een voorvertoningsscherm.

![De add gegevensinterface van de bronwerkruimte.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform detecteert automatisch eigenschapgegevens van het bestand dat u hebt geselecteerd, inclusief informatie over de gegevensindeling van het bestand, het opgegeven kolomscheidingsteken en het compressietype.

Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. Standaard wordt in de voorvertoningsinterface het eerste bestand in de geselecteerde map weergegeven.

Als u een voorvertoning van een ander bestand wilt weergeven, selecteert u het voorvertoningspictogram naast de naam van het bestand dat u wilt inspecteren.

Selecteer **[!UICONTROL Next]**.

![De pagina met gegevensvoorvertoningen van de werkruimte Bronnen.](../../../../images/tutorials/create/dlz/file-detection.png)

Raadpleeg de zelfstudie voor een gedetailleerde, stapsgewijze handleiding voor het maken van een gegevensstroom voor een bron voor cloudopslag. [een gegevensstroom voor cloudopslag maken om gegevens naar het platform te brengen](../../dataflow/batch/cloud-storage.md).

## Uw gegevens ophalen [!DNL Data Landing Zone] geloofsbrieven

[!DNL Data Landing Zone] is een bron die wordt geleverd bij uw Adobe Experience Platform Sources-licentie. [!DNL Data Landing Zone] gebruikt een SAS URI- en SAS-tokenverificatie. U kunt uw verificatiegegevens ophalen via het dialoogvenster [!UICONTROL Sources catalog] pagina.

Als u uw referenties wilt ophalen, selecteert u de **[!UICONTROL Data Landing Zone]** en kopieer vervolgens uw referenties van de rechterrail die wordt weergegeven.

![Een lijst met weergaveopties voor de landingszone voor gegevens.](../../../../images/tutorials/create/dlz/view-credentials.png)

Er wordt een pop-up weergegeven met de naam van de container, de SAS-token, de naam van de opslagaccount, de SAS-URI en de vervaldatum.

## Vernieuw uw [!DNL Data Landing Zone] geloofsbrieven

Uw [!DNL Data Landing Zone] gebruikersgegevens verlopen automatisch na 90 dagen en u moet nieuwe gegevens gebruiken om opnieuw verbinding te maken met [!DNL Data Landing Zone] na afloop. Uw gegevensstromen in Experience Platform worden niet beïnvloed door het verlopen van geloofsbrieven en u kunt nog met nieuwe en bestaande gegevensstromen met uw nieuwe geloofsbrieven blijven werken.

Er zijn twee manieren om uw [!DNL Data Landing Zone] referenties:

>[!BEGINTABS]

>[!TAB De bronkaart gebruiken]

Als u uw referenties wilt vernieuwen vanaf de pagina met de broncatalogus, selecteert u de ellipsen (**`...`**) in de [!DNL Data Landing Zone] en selecteer vervolgens **[!UICONTROL Refresh credentials]**.

![Referenties vernieuwen met de bronkaart.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Er verschijnt een pop-upvenster waarin u om bevestiging wordt gevraagd voordat u verdergaat. Wanneer u klaar bent, selecteert u **[!UICONTROL Refresh credentials]**.

![Het bevestigingsvenster voor vernieuwde referenties.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB Rechterraster gebruiken]

Als u uw referenties wilt vernieuwen met behulp van het rechterspoor, selecteert u de optie **[!UICONTROL Data Landing Zone]** bronkaart en selecteer vervolgens **[!UICONTROL More actions]**. Selecteer vervolgens **[!UICONTROL Refresh Credentials]** en bevestig vervolgens het gebruik van het pop-upvenster dat wordt weergegeven.

![Vernieuw referenties met de rechterrail.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Volgende stappen

Door deze zelfstudie te volgen hebt u toegang tot uw [!DNL Data Landing Zone] en geleerd om uw geloofsbrieven terug te winnen en te verfrissen. U kunt nu verdergaan met de volgende zelfstudie [een gegevensstroom maken om gegevens van een cloudopslag naar het platform te brengen](../../dataflow/batch/cloud-storage.md).
