---
title: Foutopsporingsmethoden
description: Leer hoe u foutopsporingsmogelijkheden in de Web SDK kunt schakelen.
keywords: foutopsporing in webSDK;foutopsporing;foutopsporingsopdracht;setDebug;debugEnabled;debug
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: aea46e3804d315c1237fc853540771f1b5c2b767
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Foutopsporingsmethoden

Wanneer het zuiveren wordt toegelaten, voert het Web SDK berichten aan de browser console uit die in het zuiveren van uw implementatie nuttig kunnen zijn. Hierdoor kunnen ook [`_satellite.logger`](../tags/logger.md) -berichten worden weergegeven als u tags gebruikt als implementatiemethode. Foutopsporing is nuttig als u wilt begrijpen hoe de SDK zich gedraagt volgens de regels en gegevenselementen die u hebt ingesteld.

Foutopsporing is standaard uitgeschakeld, maar u kunt deze op vier verschillende manieren in- of uitschakelen. U kunt om het even welke combinatie van deze methodes gebruiken om het zuiveren voor uw ontwikkelingswerkschema toe te laten of onbruikbaar te maken.

## `debugEnabled` gebruiken in de opdracht `configure`

Stel de Booleaanse waarde `debugEnabled` in op true wanneer u de extensie configureert. Deze optie wordt doorgaans gebruikt voor ontwikkelomgevingen, omdat deze foutopsporing mogelijk maakt voor iedereen die een pagina op uw site bezoekt:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

Zie [`debugEnabled`](../js/commands/configure/debugenabled.md) voor meer informatie.

## De opdracht `setDebug` gebruiken

Op dezelfde manier als bovengenoemde booleaanse, laat dit bevel het zuiveren over alle bezoekers aan de pagina toe.

```js
alloy("setDebug", {"enabled": true});
```

Zie de opdracht [`setDebug`](../js/commands/setdebug.md) voor meer informatie.

## Een parameter voor een queryreeks instellen

U kunt foutopsporing inschakelen door de querytekenreeks `?alloy_debug=true` aan het einde van een URL toe te voegen. Bijvoorbeeld:

`http://example.com/?alloy_debug=true`

Deze methode is alleen van toepassing op uw lokale computer, zodat u foutopsporing kunt toepassen op productiewebsites zonder foutopsporing voor iedereen in te schakelen. Het toelaten van het zuiveren op deze manier blijft voor de rest van uw het doorbladeren zitting of tot u het onbruikbaar maakt.

## De Adobe Experience Platform Debugger gebruiken

De Adobe Experience Platform Debugger is een krachtig hulpmiddel dat uw webpagina&#39;s controleert en u helpt bij het opsporen van fouten in uw implementatie van Experience Cloud-producten. U kunt foutopsporing inschakelen op het tabblad Configuratie van de sectie AEP Web SDK.

![ laat debugger ](../js/assets/enable-debugging.png) toe

Zie [ overzicht van Adobe Experience Platform Debugger ](/help/debugger/home.md) voor meer informatie.
