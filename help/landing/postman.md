---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;api-handleiding;platform-api-handleiding;inleiding tot platform;ontwikkelaarshandleiding
solution: Experience Platform
title: Postman in Adobe Experience Platform
description: Dit document bevat stappen waarin wordt beschreven hoe u een Postman-omgeving instelt, Postman-verzamelingen importeert en een lijst met beschikbare verzamelingen voor elke Platform-service.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Postman in Adobe Experience Platform

Postman is een samenwerkingsplatform voor API-ontwikkeling waarmee u omgevingen kunt instellen met vooraf ingestelde variabelen, API-verzamelingen kunt delen, CRUD-aanvragen kunt stroomlijnen en nog veel meer. De meeste Platform API-services hebben Postman-verzamelingen die kunnen worden gebruikt om te helpen bij het maken van API-aanroepen.

## Een Postman-omgeving instellen voor Experience Platform

De volgende videohandleiding geeft een overzicht van het maken en instellen van uw Postman-omgeving. Een Postman-omgeving bevat alle vereiste headers die u nodig hebt om API-aanroepen uit te voeren naar de verschillende hieronder vermelde verzamelingen. Zodra de opstelling, om het even welke tijd een waarde (zoals `ACCESS_TOKEN`) verloopt kunt u de huidige waarde in het milieu bijwerken, en deze nieuwe waarde wordt gebruikt over al uw inzamelingen.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-verzamelingen {#collections}

Een omslag die alle beschikbare inzamelingen van Postman bevat kan door worden gevonden, bezoekend de [ steekproeven van Postman GitHub van het Experience Platform ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Alternatief, kan een de inzamelingsverbinding van Postman in elk individueel wagerdossier in de [ API verwijzingsdocumentatie ](https://www.adobe.com/go/platform-api-reference-en) op Adobe I/O worden gevonden.

Als u een Postman-verzameling wilt downloaden, selecteert u **[!DNL Raw]** op de GitHub-pagina om het onbewerkte JSON-bestand op een nieuw tabblad te laden. Klik vervolgens met de rechtermuisknop en selecteer **[!DNL Save as]** om het bestand op te slaan naar de gewenste lokale bestemming.

![ ruwe JSON ](./images/api-guide/raw-collection.PNG)

## Een Postman-verzameling importeren {#import}

Om de inzameling van a [ Postman ](#collections) te gebruiken, moet u een milieu opstelling hebben. Nadat u de omgeving hebt ingesteld, selecteert u de **[!DNL Manage Environments]** -kiezer in de rechterbovenhoek.

![ beheert milieu selecteur ](./images/api-guide/environment-selector.png)

Er verschijnt een pop-upvenster met daarin al uw huidige omgevingen. Selecteer **[!DNL import]** als u een verzameling wilt importeren.

![ de invoerknoop ](./images/api-guide/import-collection.png)

U wordt gevraagd een bestand te kiezen dat u wilt importeren. Selecteer het Postman-verzamelingsbestand dat u wilt importeren. Als deze optie is geselecteerd, wordt de verzameling in de linkertrack gevuld onder het tabblad Verzamelingen.

![ bevolkte inzameling ](./images/api-guide/imported-collection.png)

Elke inzameling heeft verschillende zeer belangrijk-waardeparen die kunnen worden vereist om een succesvolle verrichting uit te voeren CRUD. Gelieve te herzien de de ontwikkelaarsgids van de dienst [ API ](api-guide.md#api-guides) om over vereiste waarden, uiteinden te leren, en voorbeelden te zien.

Meer over Postman UI en zijn beschikbare eigenschappen leren, bezoek de [ documentatie van Postman ](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Een toegangstoken met Postman genereren voor niet-productiegebruik

>[!WARNING]
>
>Zoals genoteerd in de inzameling van Postman van de Dienst van Identity Management (IMS), zijn de gesignaleerde generatiemethodes geschikt voor **niet-productiegebruik**. Bij lokale ondertekening wordt een JavaScript-bibliotheek geladen van een externe host en bij externe ondertekening wordt de persoonlijke sleutel verzonden naar een webservice die eigendom is van en wordt beheerd door Adobe. Hoewel deze persoonlijke sleutel niet wordt opgeslagen in de Adobe, mogen productietoetsen nooit met iemand worden gedeeld.

De video gebruikt hieronder de [ inzameling van Postman van de Dienst van Identity Management (IMS) ](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) die van de openbare bewaarplaats GitHub kan worden gedownload.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Volgende stappen

In dit document worden Postman-omgevingen, -verzamelingen en hoe verzamelingen worden geïmporteerd. Nu u klaar Postman hebt, bezoek het [ Platform begonnen gids ](api-guide.md) voor informatie over vereiste kopballen, voorbeelden, en een lijst van [ API gidsen ](api-guide.md#api-guides) beschikbaar voor elke dienst van het Platform.
