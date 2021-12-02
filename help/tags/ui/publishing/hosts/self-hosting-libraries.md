---
title: Zelf-hostingbibliotheken
description: Leer hoe u zelfhosting voor uw tagbibliotheek kunt implementeren in Adobe Experience Platform.
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: 91b28fc284344b42020b0e49b64ac023e492d572
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Bibliotheken die zichzelf hosten

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Met tags in Adobe Experience Platform kunt u een set bestanden maken die een [build](../builds.md). Deze set bestanden bepaalt het gedrag van de toepassing tijdens runtime.

Builds moeten ergens worden gehost, zodat clientapparaten ze tijdens runtime kunnen ophalen.

Platform kan het hosten van deze dossiers voor u of u leiden kunt het zelf doen.

## Beheerd door Adobe {#managed-by-adobe}

Adobe is niet bezig met webhosting. Als u verkiest om Adobe te hebben het ontvangen beheren, worden uw bouwstijlen geleverd aan een netwerk van de derdeinhoudslevering (CDN) dat wij een contract met hebben.

Momenteel is de primaire CDN-provider Akamai. Bestanden die op Akamai worden gehost, hebben een domein van `assets.adobedtm.com`.

### Waarom beheerde hosting gebruiken?

De belangrijkste reden om beheerde hosting te gebruiken is gemak. Het is eenvoudiger om de vereiste host te maken en u hoeft zich geen zorgen te maken over onderhoud.

## Zelfhosting

Als u niet wilt dat Adobe uw gehoste bestanden beheert, moet u deze zelf hosten. Om uw dossiers te ontvangen, moet u de voltooide bouwstijlen van Platform krijgen en voor het krijgen van de dossiers door de versiecyclus van uw bedrijf op bedrijf-beheerde servers verantwoordelijk zijn.

### Waarom zelfhosting gebruiken?

Er zijn een aantal redenen om ervoor te kiezen om uw eigen build-bestanden te hosten.

* Sommige browsers blokkeren het domein assets.adobedtm.com dat op de privacymontages wordt gebaseerd de eindgebruiker heeft gevormd
* Zelf-ontvangen vermindert het vereiste aantal DNS raadplegingen
* U hebt specifieke kopteksten u voor veiligheid moet plaatsen
* De vereisten voor het beheren van de cache verschillen van de standaardinstellingen voor Adobe
* U wilt meer controle over de locatie van de randknooppunten
* Uw organisatie heeft veiligheids en wettelijke vereisten die u verhinderen de Adobe-beheerde optie te gebruiken

### Hoe te om zelf-gastheer te zijn

Er zijn twee methodes u kunt gebruiken om voltooide bouwstijlen te verwerven zodat u zelf-gastheer kunt.

* Download
* Directe levering

#### Downloaden

De builds kunnen worden geleverd als een gecomprimeerd ZIP-bestand (codering optioneel). Vervolgens kunt u het pakket uitpakken en de inhoud in uw releasecyclus invoegen en deze op uw eigen servers plaatsen.

Een [Beheerd door Adobe](self-hosting-libraries.md) host en selecteer de [Archief](../environments.md) in uw omgeving. De omgeving biedt een downloadkoppeling. Wanneer een build wordt gemaakt, kunt u deze ophalen via de downloadkoppeling van de omgeving.

#### Directe levering

De builds kunnen ook rechtstreeks aan een server worden geleverd SFTP die u creeerde. U neemt de verantwoordelijkheid om deze gegevens in uw releasecyclus in te voeren en ze live te zetten.

Als u een directe levering wilt uitvoeren, moet u een [SFTP-host](sftp-host.md) en wijs die host toe aan uw omgeving. Wanneer u in die omgeving een bibliotheek maakt, worden de bestanden geleverd aan uw SFTP-server.
