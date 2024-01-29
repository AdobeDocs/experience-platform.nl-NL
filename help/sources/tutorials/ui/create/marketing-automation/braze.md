---
title: Een gegevensstroom maken voor Braze-gegevens in de gebruikersinterface
description: Leer hoe u een gegevensstroom maakt voor uw Braze-account met de gebruikersinterface van Adobe Experience Platform.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 92d3a7143edc81cc5266ef5a33a8c53dcfdf1074
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Een [!DNL Braze] bronverbinding in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Braze] De bron is in bèta. Lees de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

[!DNL Braze] maakt klantgerichte interacties tussen consumenten en merken in real time mogelijk. [!DNL Braze Currents] is een real-time gegevensstroom van betrokkenheidsgebeurtenissen van het platform van Braze dat de robuustste maar korrelige uitvoer uit het [!DNL Braze] platform.

Lees de volgende zelfstudie om te leren hoe u gegevens over betrokkenheidsgebeurtenissen van uw [!DNL Braze] account aan Adobe Experience Platform in de gebruikersinterface.

## Vereisten

Voor het uitvoeren van de stappen in deze handleiding hebt u het volgende nodig:

* Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en toestemming om een nieuwe streamingbronverbinding te maken.
* Een aanmelding bij uw [[!DNL Braze] dashboard](https://dashboard.braze.com/sign_in), een ongebruikte [Huidige-connectorlicentie](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)en machtigingen om een aansluiting te maken. Lees voor meer informatie de [vereisten voor het opzetten [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Deze zelfstudie vereist ook een goed begrip van [[!DNL Braze] Huidige](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Als u al een [!DNL Braze] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/marketing-automation.md).

## Verbind uw [!DNL Braze] account aan Experience Platform

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *Marketing Automation* categorie, selecteert u **[!UICONTROL Braze]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De broncatalogus op het Experience Platform UI met de Bron van de Huidige Bestanden van de Bouw geselecteerd.](../../../../images/tutorials/create/braze/catalog.png)

Vervolgens uploadt u de geleverde [Voorbeeldbestand Braze Currines](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Dit bestand bevat alle mogelijke velden die door Braze kunnen worden verzonden als onderdeel van een gebeurtenis.

![Het scherm &quot;Gegevens toevoegen&quot;.](../../../../images/tutorials/create/braze/select-data.png)

Zodra uw dossier wordt geupload, moet u uw gegevens verstrekken gegevensstroom, met inbegrip van informatie over uw dataset en het schema dat u aan in kaart brengt.
![Het scherm &quot;Dataflow Details&quot; markeert &quot;Dataset details&quot;.](../../../../images/tutorials/create/braze/dataflow-detail.png)

Dan, vorm afbeelding voor uw gegevens gebruikend de toewijzingsinterface.

![Het scherm &quot;Toewijzing&quot;.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>Tijdstempels voor rasteren worden niet uitgedrukt in milliseconden, maar in seconden. Als u de tijdstempels in het Experience Platform nauwkeurig wilt weergeven, moet u berekende velden maken in milliseconden. Een berekening van &quot;tijd * 1000&quot; wordt correct omgezet in milliseconden, die geschikt zijn voor toewijzing aan een tijdstempelveld binnen Experience Platform.
>
>![Een berekend veld voor een tijdstempel maken ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Vereiste referenties verzamelen

Zodra uw verbinding wordt gecreeerd, moet u de volgende credentiewaarden verzamelen, die u dan in het Dashboard van het Bol zult verstrekken om gegevens naar te verzenden [!DNL Platform]. Lees voor meer informatie de [!DNL Braze] [handleiding voor navigeren naar huidige bestanden](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Veld | Beschrijving |
| ---------- | ----------- |
| `Client ID` | De client-id die aan uw [!DNL Platform] bron. |
| `Client Secret` | Het clientgeheim dat aan uw [!DNL Platform] bron. |
| `Tenant ID` | De huurder-id die aan uw [!DNL Platform] bron. |
| `Sandbox Name` | De sandbox die aan uw [!DNL Platform] bron. |
| `Dataflow ID` | De gegevensstroom-id die aan uw [!DNL Platform] bron. |
| `Streaming Endpoint` | Het streamingeindpunt dat aan uw [!DNL Platform] bron. Merk op dat het Breken dit automatisch in de partij het stromen eindpunt zal omzetten. |

### Configureren [!DNL Braze Currents] om gegevens naar uw gegevensbron te stromen

Binnen de [!DNL Braze Dashboard], navigeren naar partnerintegratie **->** Gegevens exporteren en vervolgens selecteren **[!DNL Create New Current]**. U zal worden ertoe aangezet om een naam voor de schakelaar, contactinformatie voor berichten over de schakelaar, en de hierboven vermelde geloofsbrieven te verstrekken. Selecteer de gebeurtenissen u wenst te ontvangen, naar keuze om het even welke gewenste gebiedsuitsluitingen/transformaties vormen, en dan selecteren **[!DNL Launch Current]**.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Braze] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van het marketingautomatiseringssysteem te integreren [!DNL Platform]](../../dataflow/marketing-automation.md).