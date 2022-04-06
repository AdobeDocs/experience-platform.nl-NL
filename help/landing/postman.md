---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;api-handleiding;platform-api-handleiding;inleiding tot platform;ontwikkelaarshandleiding
solution: Experience Platform
title: Postman in Adobe Experience Platform
topic-legacy: api guide
description: Dit document bevat stappen waarin wordt beschreven hoe u een Postman-omgeving instelt, Postman-verzamelingen importeert en een lijst met beschikbare verzamelingen voor elke service van Platforms.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Postman in Adobe Experience Platform

Postman is een samenwerkingsplatform voor API-ontwikkeling waarmee u omgevingen kunt instellen met vooraf ingestelde variabelen, API-verzamelingen kunt delen, CRUD-aanvragen kunt stroomlijnen en nog veel meer. De meeste Platform API diensten hebben de inzamelingen van Postman die kunnen worden gebruikt om bij het maken van API vraag te helpen.

## Een Postman-omgeving instellen voor Experience Platform

De volgende videohandleiding geeft een overzicht van het maken en instellen van uw Postman-omgeving. Een Postman-omgeving bevat alle vereiste headers die u nodig hebt om API-aanroepen uit te voeren naar de verschillende hieronder vermelde verzamelingen. Wanneer een waarde eenmaal is ingesteld, verloopt deze altijd (bijvoorbeeld een `ACCESS_TOKEN`) kunt u de huidige waarde in de omgeving bijwerken en deze nieuwe waarde wordt gebruikt voor al uw verzamelingen.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postcollecties {#collections}

Een map met alle beschikbare Postman-verzamelingen kunt u vinden op [Experience Platform Postman samples GitHub repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). U kunt ook een Postman-verzamelingskoppeling vinden in elk afzonderlijk wagerbestand in het dialoogvenster [API-naslagdocumentatie](https://www.adobe.com/go/platform-api-reference-en) op Adobe I/O.

Als u een Postman-verzameling wilt downloaden, selecteert u **[!DNL Raw]** van de pagina GitHub om het ruwe JSON- dossier in een nieuw lusje te laden. Klik vervolgens met de rechtermuisknop en selecteer **[!DNL Save as]** om het bestand op te slaan naar een door u gekozen lokale bestemming.

![raw JSON](./images/api-guide/raw-collection.PNG)

## Een Postman-verzameling importeren {#import}

Om een [Postboeking](#collections), moet u een omgeving instellen. Als u de omgeving hebt ingesteld, selecteert u de **[!DNL Manage Environments]** in de rechterbovenhoek.

![omgevingskiezer beheren](./images/api-guide/environment-selector.png)

Er verschijnt een pop-upvenster met daarin al uw huidige omgevingen. Als u een verzameling wilt importeren, selecteert u **[!DNL import]** .

![importknop](./images/api-guide/import-collection.png)

U wordt gevraagd een bestand te kiezen dat u wilt importeren. Selecteer het Postman-verzamelingsbestand dat u wilt importeren. Als deze optie is geselecteerd, wordt de verzameling in de linkertrack gevuld onder het tabblad Verzamelingen.

![bevolkte verzameling](./images/api-guide/imported-collection.png)

Elke inzameling heeft verschillende zeer belangrijk-waardeparen die kunnen worden vereist om een succesvolle verrichting uit te voeren CRUD. Controleer de services [Handleiding voor API-ontwikkelaars](api-guide.md#api-guides) voor meer informatie over de vereiste waarden, tips en voorbeelden.

Ga voor meer informatie over de gebruikersinterface van Postman en de beschikbare functies naar de [Postman-documentatie](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Een toegangstoken met Postman genereren voor niet-productiegebruik

>[!WARNING]
>
>Zoals opgemerkt in de Adobe I/O toegangstoken van Postman inzameling, zijn de gesignaleerde generatiemethodes geschikt voor **niet-productiegebruik**. Bij lokaal ondertekenen wordt een JavaScript-bibliotheek geladen van een externe host en bij extern ondertekenen wordt de persoonlijke sleutel verzonden naar een webservice die eigendom is van en wordt beheerd door Adobe. Hoewel Adobe deze persoonlijke sleutel niet opslaat, mogen productietoetsen nooit met iemand worden gedeeld.

In de onderstaande video wordt het [Adobe I/O toegangstoken genereren, verzameling](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) die van de openbare bewaarplaats GitHub kunnen worden gedownload.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Volgende stappen

In dit document worden Postman-omgevingen, -verzamelingen en hoe verzamelingen worden geïmporteerd. Nu u klaar bent voor Postman, gaat u naar de [Aan de slag met Platform](api-guide.md) voor informatie over vereiste kopballen, voorbeelden, en een lijst van [API-hulplijnen](api-guide.md#api-guides) beschikbaar voor elke dienst van het Platform.
