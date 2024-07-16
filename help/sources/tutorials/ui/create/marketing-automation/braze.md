---
title: Een gegevensstroom maken voor Braze-gegevens in de gebruikersinterface
description: Leer hoe u een gegevensstroom maakt voor uw Braze-account met de gebruikersinterface van Adobe Experience Platform.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Een [!DNL Braze Currents] bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De bron [!DNL Braze Currents] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[!DNL Braze] maakt klantgerichte interacties tussen consumenten en merken in real-time mogelijk. [!DNL Braze Currents] is een realtime gegevensstroom van betrokkenheidsgebeurtenissen van het Braze-platform die de meest robuuste maar korrelige export van het [!DNL Braze] -platform is.

Lees de volgende zelfstudie om te leren hoe u gegevens over betrokkenheidsgebeurtenissen van uw [!DNL Braze] -account naar Adobe Experience Platform kunt overbrengen in de gebruikersinterface.

## Vereisten

Voor het uitvoeren van de stappen in deze handleiding hebt u het volgende nodig:

* Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en toestemming om een nieuwe het stromen bronverbinding tot stand te brengen.
* Login aan uw [[!DNL Braze]  dashboard ](https://dashboard.braze.com/sign_in), een ongebruikte [ vergunning van de Schakelaar van Studenten ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents), en toestemmingen om een schakelaar tot stand te brengen. Voor meer informatie, lees de [ vereisten aan opstelling  [!DNL Currents] ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Dit leerprogramma vereist ook een werkend begrip van [[!DNL Braze]  Huidige teksten ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Als u reeds een [!DNL Braze] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/marketing-automation.md).

## Sluit uw [!DNL Braze] -account aan op het Experience Platform

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *categorie van de Automatisering van de Marketing*, selecteer **[!UICONTROL Braze Currents]**, en selecteer dan **[!UICONTROL Add data]**.

![ de broncatalogus op het Experience Platform UI met de Bron van de Stroom geselecteerde Studenten.](../../../../images/tutorials/create/braze/catalog.png)

Daarna, upload het verstrekte [ de steekproefdossier van de Studenten van de Bodemo ](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Dit bestand bevat alle mogelijke velden die door Braze kunnen worden verzonden als onderdeel van een gebeurtenis.

![ het scherm &quot;voegt Gegevens&quot;toe.](../../../../images/tutorials/create/braze/select-data.png)

Zodra uw dossier wordt geupload, moet u uw gegevens verstrekken gegevensstroom, met inbegrip van informatie over uw dataset en het schema dat u aan in kaart brengt.
![ het scherm &quot;Dataflow Details&quot;het benadrukken van &quot;de details van de Dataset.&quot;](../../../../images/tutorials/create/braze/dataflow-detail.png)

Dan, vorm afbeelding voor uw gegevens gebruikend de toewijzingsinterface.

![ het scherm van de &quot;Afbeelding&quot;.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>Tijdstempels voor rasteren worden niet uitgedrukt in milliseconden, maar in seconden. Als u de tijdstempels in het Experience Platform nauwkeurig wilt weergeven, moet u berekende velden maken in milliseconden. Een berekening van &quot;tijd * 1000&quot; wordt correct omgezet in milliseconden, die geschikt zijn voor toewijzing aan een tijdstempelveld binnen Experience Platform.
>
>![ Creërend een berekend gebied voor timestamp ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Vereiste referenties verzamelen

Zodra uw verbinding wordt gecreeerd, moet u de volgende credentiewaarden verzamelen, die u dan in het Braze Dashboard zult verstrekken om gegevens naar Experience Platform te verzenden. Voor meer informatie, leest de [!DNL Braze] [ gids bij het navigeren aan Huidige heden ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Veld | Beschrijving |
| --- | --- |
| Client-id | De client-id die aan de bron van het Experience Platform is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan de bron van het Experience Platform is gekoppeld. |
| Tenant-id | De huurder-id die aan uw bron van het Experience Platform is gekoppeld. |
| Naam sandbox | De sandbox die aan de bron van het Experience Platform is gekoppeld. |
| Dataflow-id | De gegevensstroom-id die aan de bron van het Experience Platform is gekoppeld. |
| Streaming eindpunt | Het streamingeindpunt dat aan de bron van het Experience Platform is gekoppeld. **Nota**: [!DNL Braze] zet automatisch dit in het batch die eindpunt stromen om. |

### Configureer [!DNL Braze Currents] om gegevens te streamen naar uw gegevensbron

Binnen [!DNL Braze Dashboard], navigeer aan de Integraties van de Partner **->** de Uitvoer van Gegevens, dan uitgezochte **[!DNL Create New Current]**. U zal worden ertoe aangezet om een naam voor de schakelaar, contactinformatie voor berichten over de schakelaar, en de hierboven vermelde geloofsbrieven te verstrekken. Selecteer de gebeurtenissen die u wilt ontvangen, configureer desgewenst alle gewenste velduitsluitingen/transformaties en selecteer vervolgens **[!DNL Launch Current]** .

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Braze] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om het systeemgegevens van de marketing automatisering in  [!DNL Platform]](../../dataflow/marketing-automation.md) te brengen.
