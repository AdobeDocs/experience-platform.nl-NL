---
title: Ondersteunende toestemming
seo-title: Voorkeur voor webSDK van Adobe Experience Platform ondersteunen
description: Leer hoe u toestemmingsvoorkeuren met Experience Platform Web SDK kunt ondersteunen
seo-description: Leer hoe u toestemmingsvoorkeuren met Experience Platform Web SDK kunt ondersteunen
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Ondersteunende toestemming

Om de privacy van uw gebruiker te respecteren, zou u om de toestemming van de gebruiker kunnen willen vragen alvorens SDK toe te staan om gebruiker-specifieke gegevens voor bepaalde doeleinden te gebruiken. Momenteel staat SDK gebruikers alleen toe om in of uit alle doeleinden te kiezen, maar in de toekomst hoopt Adobe meer korrelige controle over specifieke doeleinden te verschaffen.

Als de gebruiker voor alle doeleinden inbelt, mag de SDK de volgende taken uitvoeren:

* Gegevens verzenden van en naar Adobe-servers.
* Cookies of webopslagitems lezen en schrijven (behalve voor het doorlopen van de aanmeldingsvoorkeuren van de gebruiker).

Als de gebruiker uit alle doeleinden kiest, voert de SDK geen van deze taken uit.

## Toestemming configureren

De gebruiker is standaard voor alle doeleinden ingeschakeld. Als u wilt voorkomen dat de SDK de bovenstaande taken uitvoert totdat de gebruiker het programma inschakelt, geeft u als volgt `"defaultConsent": { "general": "pending" }` tijdens de SDK-configuratie door:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Wanneer de standaardtoestemming voor het algemene doel op in behandeling wordt geplaatst, leidt het proberen om het even welke bevelen uit te voeren die van gebruiker opt-in voorkeur (bijvoorbeeld, het `event` bevel) afhangen tot het bevel dat binnen SDK een rij wordt gevormd. Deze opdrachten worden pas verwerkt nadat u de aanmeldingsvoorkeuren van de gebruiker aan de SDK hebt doorgegeven.

Op dit punt wilt u de gebruiker wellicht vragen zich ergens in de gebruikersinterface aan te melden. Nadat de gebruikersvoorkeuren zijn verzameld, geeft u deze door aan de SDK.

## Voorkeuren voor toestemming communiceren

Als de gebruiker binnen kiest, voer het `setConsent` bevel met de `general` optie uit die aan `in` als volgt wordt geplaatst:

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "in" 
      }
    }]
});
```

Omdat de gebruiker nu heeft gekozen, voert de SDK alle eerder in de wachtrij geplaatste opdrachten uit. Toekomstige opdrachten die afhankelijk zijn van het inchecken door de gebruiker, worden _niet_ in de wachtrij geplaatst en worden direct uitgevoerd.

Als de gebruiker ervoor kiest om te weigeren, voert u de `setConsent` opdracht uit met de `general` optie ingesteld op `out` als volgt:

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "out" 
      }
    }]
});
```

>[!NOTE]
>
>Nadat een gebruiker heeft gekozen, zal SDK u niet toestaan om de gebruikers toestemming te plaatsen aan `in`.

Omdat de gebruiker ervoor koos om te weigeren, worden de beloftes die van eerder een rij vormde bevelen zijn teruggekeerd verworpen. Toekomstige opdrachten die afhankelijk zijn van de gebruiker die incheckt, retourneren beloftes die op dezelfde manier worden afgewezen. Raadpleeg Opdrachten [uitvoeren voor meer informatie over het afhandelen of onderdrukken van fouten](executing-commands.md).

>[!NOTE]
>
>Momenteel ondersteunt de SDK alleen het `general` doel. Hoewel wij van plan zijn een robuustere reeks doelen of categorieën te ontwikkelen die aan de verschillende mogelijkheden en productaanbiedingen van de Adobe zullen beantwoorden, is de huidige implementatie een alles of niets benadering van opt-in.  Dit geldt alleen voor het Adobe Experience Platform [!DNL Web SDK] en NIET voor andere Adobe JavaScript-bibliotheken.

## Voorkeuren voor blijvende toestemming

Nadat u gebruikersvoorkeuren aan de SDK hebt doorgegeven met de `setConsent` opdracht, blijft de SDK de gebruikersvoorkeuren voor een cookie gebruiken. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de SDK deze voorkeuren op en gebruikt deze. U hoeft de `setConsent` opdracht niet opnieuw uit te voeren, behalve om een wijziging in de gebruikersvoorkeuren door te geven, die u op elk gewenst moment kunt doorvoeren.