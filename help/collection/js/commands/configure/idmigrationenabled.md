---
title: idMigrationEnabled
description: Hiermee kan de Web SDK AMCV-cookies lezen.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

Met de eigenschap `idMigrationEnabled` kan de Web SDK AMCV-cookies lezen die zijn ingesteld door eerdere Adobe Experience Cloud-implementaties. Als uw organisatie uw implementatie aan het Web SDK bevordert, staat dit het plaatsen een vlottere overgang aan de huidige dienst van identiteitskaart van Adobe Experience Cloud toe. Deze instelling is waardevol, zodat u geen sterke toename ziet van unieke bezoekers wanneer u een upgrade uitvoert naar de Web SDK.

Als uw organisatie een nieuwe implementatie van SDK van het Web in werking stelt, heeft het toelaten van dit plaatsen geen invloed op gegevensinzameling of bezoekersidentificatie. Er zijn geen nadelen om het voor alle implementaties toe te laten.

## Hoe identiteitsmigratie werkt {#how-it-works}

De bezoeker-API slaat de Experience Cloud-id (ECID) op in een cookie met de naam `AMCV_<ORG_ID>` . Wanneer `idMigrationEnabled` `true` is (de standaardwaarde), leest de Web SDK automatisch de ECID uit het cookie AMCV en gebruikt deze als de identiteit van de bezoeker op het eerste Edge Network-verzoek.

1. Een bezoeker komt op een pagina aan die nu de Web SDK in plaats van de Bezoeker API gebruikt.
1. De Web SDK controleert of er een bestaand `kndctr_` identiteitscookie (zijn eigen cookie-indeling) is. Als er geen wordt gevonden, zoekt het naar een `AMCV_` cookie.
1. Als een `AMCV_` -cookie wordt gevonden, extraheert de Web SDK de ECID en gebruikt deze om de identiteit van de bezoeker te initialiseren.
1. De Web SDK stelt een nieuw `kndctr_` identiteitscookie in met dezelfde ECID.
1. Bij volgende bezoeken gebruikt de Web SDK het `kndctr_` cookie rechtstreeks. Het `AMCV_` -cookie is niet meer nodig.

Om migratie te laten werken, moet de Web SDK worden geconfigureerd met dezelfde [`orgId`](/help/collection/js/commands/configure/orgid.md) als de Bezoeker-API heeft gebruikt en moeten deze worden geïmplementeerd op hetzelfde domein (of een subdomein van hetzelfde bovenliggende domein) waar het AMCV-cookie is ingesteld.

## Ondersteunde migratiescenario&#39;s

ID-migratie ondersteunt de volgende overgangspatronen:

* **sommige pagina&#39;s gebruiken nog Bezoeker API terwijl andere pagina&#39;s Web SDK** gebruiken: SDK leest bestaande koekjes AMCV en schrijft een nieuw koekje met bestaande ECID. Er worden ook AMCV-cookies geschreven, zodat pagina&#39;s die nog steeds de API voor bezoekers gebruiken dezelfde bezoeker blijven herkennen.
* **SDK van het Web en Bezoeker API zijn allebei aanwezig op de zelfde pagina**: Als het koekje AMCV niet wordt geplaatst, zoekt SDK Bezoeker API op de pagina en gebruikt het om ECID te krijgen.
* **de plaats is volledig naar SDK van het Web** bewogen: U kunt migratie verlaten die voor een periode wordt toegelaten zodat behouden de bestaande op AMCV-Gebaseerde bezoekers continuïteit terwijl hun koekjes worden overgezet.

>[!IMPORTANT]
>
>Laad de API voor bezoekers en de Web SDK niet tegelijkertijd op dezelfde pagina, tenzij u hebt bevestigd dat het cookie AMCV al is ingesteld. Het uitvoeren van beide bibliotheken op één pagina kan rassenvoorwaarden veroorzaken waarbij elke bibliotheek probeert om identiteit onafhankelijk te beheren, waardoor mogelijk dubbele of conflicterende ECID&#39;s worden gegenereerd.

## Migratie uitschakelen {#turn-off-migration}

Nadat uw gehele site op de Web SDK is uitgevoerd en geen bezoekers alleen een `AMCV_` -cookie hebben zonder bijbehorende `kndctr_` -cookie, kunt u identiteitsmigratie veilig uitschakelen door `idMigrationEnabled` in te stellen op `false` . Dit is een kleine optimalisatie van de prestaties en verkleint het oppervlak van uw identiteitslogica.

Als richtlijn kunt u wachten tot de maximale levensduur van het AMCV-cookie is verstreken nadat de laatste pagina is gemigreerd. Als uw AMCV-cookies twee jaar verlopen, wacht u twee jaar nadat de laatste pagina naar de Web SDK is gesneden. In de praktijk maken de meeste organisaties de migratie eerder (na een paar maanden) uit en accepteren zij een verwaarloosbare inflatie van het kleine aantal bezoekers dat na een lange afwezigheid voor het eerst terugkeert.

## Audience Manager trait updates

Wanneer gegevens met XDM-indeling tijdens de migratie naar Audience Manager worden verzonden, moeten die gegevens in signalen worden omgezet. Uw kenmerken moeten worden bijgewerkt om de nieuwe sleutels te weerspiegelen die door XDM worden verstrekt. Dit proces wordt gemakkelijker gemaakt door het [&#x200B; hulpmiddel BAAAM &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) te gebruiken.

## Migratie van id&#39;s van derden {#third-party-id}

Als in uw API-implementatie van de bezoeker id&#39;s van derden zijn gebruikt (het `demdex.net` -cookie), kan de Web SDK deze ook migreren. Configureer [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) naar `true` in uw Web SDK-configuratie. Het Web SDK leest het bestaande demdex-cookie en neemt de identiteit van een derde op in haar Edge Network-aanvragen, volgens hetzelfde migratiepatroon als het AMCV-cookie.

## Validatie {#validation}

Controleren of identiteitsmigratie correct werkt:

1. Open een pagina die eerder de Bezoeker-API gebruikte (nu de Web SDK gebruikt) in een browser met een bestaande `AMCV_` -cookie.
2. Controleer in de ontwikkelaars of er een `kndctr_` identiteitscookie is ingesteld en of de ECID overeenkomt met de cookie in het `AMCV_` -cookie.
3. Vergelijk na de implementatie het aantal unieke bezoekers voor en na de migratie gedurende dezelfde periode. Een aanzienlijke toename van unieke bezoekers kan erop wijzen dat migratie geen identiteiten naar voren brengt.

>[!TIP]
>
>Gebruik `getIdentity` om de ECID voor vergelijking programmatisch op te halen:
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## Configureren `idMigrationEnabled` {#configure}

Stel de Booleaanse waarde `idMigrationEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze eigenschap in als u de mogelijkheid wilt uitschakelen om AMCV-cookies te lezen die zijn ingesteld door de Bezoeker-API. De meeste organisaties hoeven dit bezit niet te plaatsen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Migratie van bezoekersidentiteitskaart inschakelen met de Web SDK-tagextensie

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [&#x200B; de configuratiemontages van de Identiteit &#x200B;](/help/tags/extensions/client/web-sdk/configure/identity.md).
