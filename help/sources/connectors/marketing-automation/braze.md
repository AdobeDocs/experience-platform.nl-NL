---
title: Braze Current Source - Overzicht
description: Leer hoe u gegevens kunt streamen van Braze Currents naar Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>De bron [!DNL Braze Currents] is in bèta. Gelieve te lezen het [&#x200B; overzicht van bronnen &#x200B;](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens in streaming toepassingen. Ondersteuning voor streamingproviders omvat [!DNL Braze Currents] .

[!DNL Braze] maakt klantgerichte interacties tussen consumenten en merken in real-time mogelijk. [!DNL Braze Currents] is een realtime gegevensstroom van betrokkenheidsgebeurtenissen van het Braze-platform die de meest robuuste maar korrelige export van het [!DNL Braze] -platform is.

## Vereisten

Voor het uitvoeren van de stappen in deze handleiding hebt u het volgende nodig:

* Login aan [&#x200B; Adobe Experience Platform &#x200B;](https://platform.adobe.com) en toestemming om een nieuwe het stromen bronverbinding tot stand te brengen.
* Login aan uw [[!DNL Braze]  dashboard &#x200B;](https://dashboard.braze.com/sign_in), een ongebruikte [&#x200B; vergunning van de Schakelaar van Studenten &#x200B;](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents), en toestemmingen om een schakelaar tot stand te brengen. Voor meer informatie, lees de [&#x200B; vereisten aan opstelling  [!DNL Currents] &#x200B;](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Vereiste referenties verzamelen

Als u uw [!DNL Braze Currents] -gegevens naar Experience Platform wilt verzenden, moet u de volgende Experience Platform-referenties invoeren in het [!DNL Braze] UI-dashboard.

| Veld | Beschrijving |
| --- | --- |
| Client-id | De client-id die aan uw Experience Platform-bron is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan uw Experience Platform-bron is gekoppeld. |
| Tenant-id | De huurder-id die aan uw Experience Platform-bron is gekoppeld. |
| Naam sandbox | De sandbox die aan uw Experience Platform-bron is gekoppeld. |
| Dataflow-id | De gegevensstroom-id die aan uw Experience Platform-bron is gekoppeld. |
| Streaming eindpunt | Het streamingeindpunt dat aan uw Experience Platform-bron is gekoppeld. **Nota**: [!DNL Braze] zet automatisch dit in het batch die eindpunt stromen om. |

Voor informatie over hoe te om deze waarden terug te winnen, lees de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../landing/api-authentication.md). Voor informatie bij het gebruiken van het [!DNL Braze] dashboard, lees de [!DNL Braze] gids over hoe te [&#x200B; aan Huidige Bestanden &#x200B;](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents) navigeren.

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid die nodig zijn om gegevens te kunnen streamen van uw [!DNL Braze Currents] -account naar Experience Platform. U kunt aan de gids nu te werk gaan op [&#x200B; verbindend  [!DNL Braze Currents]  met Experience Platform gebruikend het gebruikersinterface &#x200B;](../../tutorials/ui/create/marketing-automation/braze.md).
