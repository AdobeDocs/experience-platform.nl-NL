---
title: Braze Current Source - Overzicht
description: Leer hoe u gegevens kunt streamen van Braze Currents naar Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>De bron [!DNL Braze Currents] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens in streaming toepassingen. Ondersteuning voor streamingproviders omvat [!DNL Braze Currents] .

[!DNL Braze] maakt klantgerichte interacties tussen consumenten en merken in real-time mogelijk. [!DNL Braze Currents] is een realtime gegevensstroom van betrokkenheidsgebeurtenissen van het Braze-platform die de meest robuuste maar korrelige export van het [!DNL Braze] -platform is.

## Vereisten

Voor het uitvoeren van de stappen in deze handleiding hebt u het volgende nodig:

* Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en toestemming om een nieuwe het stromen bronverbinding tot stand te brengen.
* Login aan uw [[!DNL Braze]  dashboard ](https://dashboard.braze.com/sign_in), een ongebruikte [ vergunning van de Schakelaar van Studenten ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents), en toestemmingen om een schakelaar tot stand te brengen. Voor meer informatie, lees de [ vereisten aan opstelling  [!DNL Currents] ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Vereiste referenties verzamelen

Als u de [!DNL Braze Currents] -gegevens naar het Experience Platform wilt verzenden, moet u de volgende referenties voor het Experience Platform invoeren in het [!DNL Braze] UI-dashboard.

| Veld | Beschrijving |
| --- | --- |
| Client-id | De client-id die aan de bron van het Experience Platform is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan de bron van het Experience Platform is gekoppeld. |
| Tenant-id | De huurder-id die aan uw bron van het Experience Platform is gekoppeld. |
| Naam sandbox | De sandbox die aan de bron van het Experience Platform is gekoppeld. |
| Dataflow-id | De gegevensstroom-id die aan de bron van het Experience Platform is gekoppeld. |
| Streaming eindpunt | Het streamingeindpunt dat aan de bron van het Experience Platform is gekoppeld. **Nota**: [!DNL Braze] zet automatisch dit in het batch die eindpunt stromen om. |

Voor informatie over hoe te om deze waarden terug te winnen, lees de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-authentication.md). Voor informatie bij het gebruiken van het [!DNL Braze] dashboard, lees de [!DNL Braze] gids over hoe te [ aan Huidige Bestanden ](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents) navigeren.

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid die nodig zijn om gegevens te kunnen streamen van uw [!DNL Braze Currents] -account naar het Experience Platform. U kunt aan de gids nu te werk gaan op [ verbindend  [!DNL Braze Currents]  met Experience Platform gebruikend het gebruikersinterface ](../../tutorials/ui/create/marketing-automation/braze.md).
