---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;api-handleiding;platform-api-handleiding;inleiding tot platform;ontwikkelaarsgids
solution: Experience Platform
title: Postman in Adobe Experience Platform
description: Dit document bevat stappen waarin wordt beschreven hoe u een Postman-omgeving instelt, Postman-verzamelingen importeert en een lijst met beschikbare verzamelingen voor elke Experience Platform-service.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Postman in Adobe Experience Platform

Postman is een samenwerkingsplatform voor API-ontwikkeling waarmee u omgevingen kunt instellen met vooraf ingestelde variabelen, API-verzamelingen kunt delen, CRUD-aanvragen kunt stroomlijnen en nog veel meer. De meeste Experience Platform API-services beschikken over Postman-verzamelingen die kunnen worden gebruikt als hulpmiddel bij het maken van API-aanroepen.

## Een Postman-omgeving instellen voor Experience Platform

De volgende videohandleiding geeft een overzicht van het maken en instellen van uw Postman-omgeving. Een Postman-omgeving bevat alle vereiste headers die u nodig hebt om API-aanroepen uit te voeren naar de verschillende hieronder vermelde verzamelingen. Zodra de opstelling, om het even welke tijd een waarde (zoals `ACCESS_TOKEN`) verloopt kunt u de huidige waarde in het milieu bijwerken, en deze nieuwe waarde wordt gebruikt over al uw inzamelingen.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-verzamelingen {#collections}

Een omslag die alle beschikbare inzamelingen van Postman bevat kan door worden gevonden, bezoekend de [&#x200B; Postman steekproeven GitHub bewaarplaats van Experience Platform &#x200B;](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Alternatief, kan een de inzamelingsverbinding van Postman in elk individueel wagerdossier in de [&#x200B; API verwijzingsdocumentatie &#x200B;](https://www.adobe.com/go/platform-api-reference-en) op Adobe I/O worden gevonden.

Als u een Postman-verzameling wilt downloaden, selecteert u **[!DNL Raw]** op de GitHub-pagina om het onbewerkte JSON-bestand op een nieuw tabblad te laden. Klik vervolgens met de rechtermuisknop en selecteer **[!DNL Save as]** om het bestand op te slaan naar de gewenste lokale bestemming.

![&#x200B; ruwe JSON &#x200B;](./images/api-guide/raw-collection.PNG)

## Een Postman-verzameling importeren {#import}

Om de inzameling van a [&#x200B; Postman &#x200B;](#collections) te gebruiken, moet u een milieu opstelling hebben. Nadat u de omgeving hebt ingesteld, selecteert u de **[!DNL Manage Environments]** -kiezer in de rechterbovenhoek.

![&#x200B; beheert milieu selecteur &#x200B;](./images/api-guide/environment-selector.png)

Er verschijnt een pop-upvenster met daarin al uw huidige omgevingen. Selecteer **[!DNL import]** als u een verzameling wilt importeren.

![&#x200B; de invoerknoop &#x200B;](./images/api-guide/import-collection.png)

U wordt gevraagd een bestand te kiezen dat u wilt importeren. Selecteer het Postman-verzamelingsbestand dat u wilt importeren. Als deze optie is geselecteerd, wordt de verzameling in de linkertrack gevuld onder het tabblad Verzamelingen.

![&#x200B; bevolkte inzameling &#x200B;](./images/api-guide/imported-collection.png)

Elke inzameling heeft verschillende zeer belangrijk-waardeparen die kunnen worden vereist om een succesvolle verrichting uit te voeren CRUD. Gelieve te herzien de de ontwikkelaarsgids van de dienst [&#x200B; API &#x200B;](api-guide.md#api-guides) om over vereiste waarden, uiteinden te leren, en voorbeelden te zien.

Meer over Postman UI en zijn beschikbare eigenschappen leren, bezoek de [&#x200B; documentatie van Postman &#x200B;](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Een toegangstoken met Postman genereren voor niet-productiegebruik

>[!WARNING]
>
>Zoals genoteerd in de inzameling van Postman van de Dienst van Identity Management (IMS), zijn de gesignaleerde generatiemethodes geschikt voor **niet-productiegebruik**. Bij lokale ondertekening wordt een JavaScript-bibliotheek geladen van een externe host en bij externe ondertekening wordt de persoonlijke sleutel verzonden naar een webservice die eigendom is van en wordt beheerd door Adobe. Hoewel Adobe deze persoonlijke sleutel niet opslaat, mogen productietoetsen nooit met iemand worden gedeeld.

De video gebruikt hieronder de [&#x200B; inzameling van Postman van de Dienst van Identity Management (IMS) &#x200B;](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) die van de openbare bewaarplaats GitHub kan worden gedownload.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Volgende stappen

In dit document worden Postman-omgevingen, -verzamelingen en hoe verzamelingen worden geïmporteerd. Nu u klaar Postman hebt, bezoek [&#x200B; Experience Platform begonnen gids &#x200B;](api-guide.md) voor informatie over vereiste kopballen, voorbeelden, en een lijst van [&#x200B; API gidsen &#x200B;](api-guide.md#api-guides) beschikbaar voor elke dienst van Experience Platform.
