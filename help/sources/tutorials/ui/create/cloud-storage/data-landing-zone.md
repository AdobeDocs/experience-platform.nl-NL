---
title: Gegevenslandingszone verbinden met platform via de gebruikersinterface
description: Leer hoe te om een van de Bron van de Gebied van Gegevens te creëren die de gebruikersinterface van het Platform gebruiken.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# Verbinding maken [!DNL Data Landing Zone] met platform via de gebruikersinterface

>[!IMPORTANT]
>
>Deze pagina is specifiek voor de [!DNL Data Landing Zone] *bron* schakelaar in Experience Platform. Voor informatie bij het verbinden met de [!DNL Data Landing Zone] *bestemmings* schakelaar, verwijs naar de [[!DNL Data Landing Zone]  pagina van de bestemmingsdocumentatie ](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] is een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden die naar Adobe Experience Platform kunnen worden overgebracht. Gegevens worden automatisch na zeven dagen uit de [!DNL Data Landing Zone] verwijderd.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Data Landing Zone] bronverbinding met behulp van de gebruikersinterface van Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Breng uw bestanden van [!DNL Data Landing Zone] naar het platform

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL cloud storage] de optie [!DNL Data Landing Zone] en selecteer vervolgens **[!UICONTROL Add data]** .

![ de broncatalogus met Gegevens die Gebied Landing selecteerde.](../../../../images/tutorials/create/dlz/catalog.png)

De stap [!UICONTROL Add data] wordt weergegeven en biedt u een interface voor het selecteren en voorvertonen van de gegevens die u naar Platform wilt verzenden.

* Het linkerdeel van de interface is een omslagbrowser, die u van een lijst van dossiers van uw container voorziet die u dan aan Platform kunt brengen.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een compatibel bestand voorvertonen.

Selecteer het bestand dat u naar het Experience Platform wilt brengen en wacht een paar minuten totdat de rechterinterface wordt bijgewerkt in een voorvertoningsscherm.

![ voegt gegevensinterface van de bronwerkruimte toe.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform detecteert automatisch eigenschapgegevens van het bestand dat u hebt geselecteerd, inclusief informatie over de gegevensindeling van het bestand, het opgegeven kolomscheidingsteken en het compressietype.

Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. Standaard wordt in de voorvertoningsinterface het eerste bestand in de geselecteerde map weergegeven.

Als u een voorvertoning van een ander bestand wilt weergeven, selecteert u het voorvertoningspictogram naast de naam van het bestand dat u wilt inspecteren.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ de pagina van de gegevensvoorproef van de bronwerkruimte.](../../../../images/tutorials/create/dlz/file-detection.png)

Voor een gedetailleerde, geleidelijke gids op hoe te om een dataflow voor een bron van de wolkenopslag tot stand te brengen, zie het leerprogramma op [ creërend een dataflow van de wolkenopslag om gegevens aan Platform ](../../dataflow/batch/cloud-storage.md) te brengen.

## Uw [!DNL Data Landing Zone] -gegevens ophalen

[!DNL Data Landing Zone] is een bron die wordt geleverd bij uw Adobe Experience Platform Sources-licentie. [!DNL Data Landing Zone] gebruikt een op SAS URI en SAS Token gebaseerde verificatie. U kunt uw verificatiegegevens ophalen van de pagina [!UICONTROL Sources catalog] .

Als u uw referenties wilt ophalen, selecteert u de **[!UICONTROL Data Landing Zone]** -kaart en kopieert u uw referenties vanuit de rechtertrack die wordt weergegeven.

![ een lijst van meningsopties voor Gegevens die Zone landen.](../../../../images/tutorials/create/dlz/view-credentials.png)

Er wordt een pop-up weergegeven met de naam van de container, de SAS-token, de naam van de opslagaccount, de SAS-URI en de vervaldatum.

## Uw [!DNL Data Landing Zone] -referenties vernieuwen

Uw [!DNL Data Landing Zone] -referenties zijn ingesteld op automatisch verlopen na 90 dagen en u moet nieuwe gegevens gebruiken om na het verlopen opnieuw verbinding te maken met [!DNL Data Landing Zone] . Uw gegevensstromen in Experience Platform worden niet beïnvloed door het verlopen van geloofsbrieven en u kunt nog met nieuwe en bestaande gegevensstromen met uw nieuwe geloofsbrieven blijven werken.

U kunt uw [!DNL Data Landing Zone] -gegevens op twee manieren vernieuwen:

>[!BEGINTABS]

>[!TAB  Gebruik de bronkaart ]

Als u uw referenties wilt vernieuwen vanaf de pagina met de broncatalogus, selecteert u de ovalen (**`...`**) in de [!DNL Data Landing Zone] -kaart en selecteert u vervolgens **[!UICONTROL Refresh credentials]** .

![ verfrist geloofsbrieven gebruikend de bronkaart.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Er verschijnt een pop-upvenster waarin u om bevestiging wordt gevraagd voordat u verdergaat. Wanneer u klaar bent, selecteert u **[!UICONTROL Refresh credentials]** .

![ verfrist zich het venster van de geloofsbevestiging.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB  Gebruik het juiste spoor ]

Als u uw referenties wilt vernieuwen met behulp van het rechterspoor, selecteert u de **[!UICONTROL Data Landing Zone]** bronkaart en vervolgens **[!UICONTROL More actions]** . Selecteer vervolgens **[!UICONTROL Refresh Credentials]** en bevestig het venster met het pop-upvenster dat wordt weergegeven.

![ verfrist geloofsbrieven gebruikend het juiste spoor.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Volgende stappen

Door deze zelfstudie te volgen, hebt u toegang tot uw [!DNL Data Landing Zone] -container en hebt u geleerd uw referenties op te halen en te vernieuwen. U kunt aan het volgende leerprogramma nu te werk gaan [ creërend een dataflow om gegevens van een wolkenopslag aan Platform ](../../dataflow/batch/cloud-storage.md) te brengen.
