---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform van 8 april 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 38acbb4a0130763fe0c565215eda7c0713e1ff6e

---


# Opmerkingen bij de release Adobe Experience Platform

## Releasedatum: 8 april 2020

## Toegangsbeheer

Experience Platform gebruikt [Adobe Admin Console](https://adminconsole.adobe.com) -productprofielen om gebruikers te koppelen aan machtigingen en sandboxen. De toestemmingen controleren toegang tot een verscheidenheid van de mogelijkheden van het Platform, met inbegrip van gegevensmodellering, profielbeheer, en zandbakbeleid.

### Belangrijkste kenmerken

| Functie | Beschrijving |
|--- | ---|
| Machtigingen | In de beheerconsole kunt u op het tabblad _Machtigingen_ in een productprofiel van het platform aanpassen welke platformmogelijkheden beschikbaar zijn voor de gebruikers die aan dat profiel zijn gekoppeld. Beschikbare machtigingscategorieën zijn: Gegevensmodellering, gegevensbeheer, profielbeheer, identiteiten, gegevenscontrole, Sandbox-beheer, doelen, bronnen. |
| Toegang tot sandboxen | Met het tabblad _Machtigingen_ in een productprofiel van het platform kunnen gebruikers toegang krijgen tot specifieke sandboxen. Zie de sectie over [sandboxen](#sandboxes) hieronder voor meer informatie. |

Zie het overzicht [van](../../access-control/home.md)toegangsbeheer voor meer informatie.

## Sandboxen

Het Experience Platform is ontworpen om toepassingen voor digitale ervaringen wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt het Experience Platform sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Belangrijkste kenmerken

| Functie | Beschrijving |
|--- | ---|
| Productiesandbox | Experience Platform beschikt over één productiesandbox die niet kan worden verwijderd of opnieuw ingesteld. |
| Niet-productie sandboxen | Er kunnen meerdere niet-productiesandboxen worden gemaakt voor één platforminstantie, zodat u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit van invloed is op uw productiesandbox. |
| Sandboxschakelaar | In de gebruikersinterface van het Platform van de Ervaring, staat de zandbakschakelaar in de bovenkant-linkerhoek van het scherm u toe om tussen beschikbare zandbakken door een dropdown menu te schakelen. |
| `x-sandbox-name` header | Alle aanroepen naar Experience Platform API&#39;s moeten nu de nieuwe `x-sandbox-name` header bevatten, waarvan de waarde verwijst naar het `name` kenmerk van de sandbox waarin de bewerking plaatsvindt. |

Zie het [sandboxoverzicht](../../sandboxes/home.md)voor meer informatie.