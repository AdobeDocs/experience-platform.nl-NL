---
title: Overzicht van Bron van Braze
description: Leer hoe u gegevens kunt streamen van Braze Currents naar Experience Platform.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>De [!DNL Braze Currents] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens in streaming toepassingen. Ondersteuning voor streamingproviders omvat [!DNL Braze Currents].

[!DNL Braze] maakt klantgerichte interacties tussen consumenten en merken in real time mogelijk. [!DNL Braze Currents] is een real-time gegevensstroom van betrokkenheidsgebeurtenissen van het platform van Braze dat de robuustste maar korrelige uitvoer uit het [!DNL Braze] platform.

## Vereisten

Voor het uitvoeren van de stappen in deze handleiding hebt u het volgende nodig:

* Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en toestemming om een nieuwe streamingbronverbinding te maken.
* Een aanmelding bij uw [[!DNL Braze] dashboard](https://dashboard.braze.com/sign_in), een ongebruikte [Huidige-connectorlicentie](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)en machtigingen om een aansluiting te maken. Lees voor meer informatie de [vereisten voor het opzetten [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Vereiste referenties verzamelen

Als u uw [!DNL Braze Currents] gegevens aan Experience Platform, moet u de volgende geloofsbrieven van het Experience Platform in [!DNL Braze] UI-dashboard.

| Veld | Beschrijving |
| --- | --- |
| Client-id | De client-id die aan de bron van het Experience Platform is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan de bron van het Experience Platform is gekoppeld. |
| Tenant-id | De huurder-id die aan uw bron van het Experience Platform is gekoppeld. |
| Naam sandbox | De sandbox die aan de bron van het Experience Platform is gekoppeld. |
| Dataflow-id | De gegevensstroom-id die aan de bron van het Experience Platform is gekoppeld. |
| Streaming eindpunt | Het streamingeindpunt dat aan de bron van het Experience Platform is gekoppeld. **Opmerking**: [!DNL Braze] zet dit automatisch om in het batch streaming eindpunt. |

Voor informatie over het ophalen van deze waarden leest u de handleiding op [aan de slag met platform-API&#39;s](../../../landing/api-authentication.md). Voor informatie over het gebruik van de [!DNL Braze] dashboard, lees de [!DNL Braze] gids over hoe te [Navigeren naar huidige](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid die nodig zijn om gegevens te kunnen streamen van uw [!DNL Braze Currents] aan Experience Platform. U kunt nu doorgaan naar de handleiding op [verbinden [!DNL Braze Currents] naar Experience Platform via de gebruikersinterface](../../tutorials/ui/create/marketing-automation/braze.md).