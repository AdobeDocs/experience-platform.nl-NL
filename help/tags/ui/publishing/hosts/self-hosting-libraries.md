---
title: Zelf-hostingbibliotheken
description: Leer hoe u zelfhosting voor uw tagbibliotheek kunt implementeren in Adobe Experience Platform.
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Bibliotheken die zichzelf hosten

De markeringen in Adobe Experience Platform staan voor de productie van een reeks dossiers toe genoemd a [&#x200B; bouwt &#x200B;](../builds.md). Deze set bestanden bepaalt het gedrag van de toepassing tijdens runtime.

Builds moeten ergens worden gehost, zodat clientapparaten ze tijdens runtime kunnen ophalen.

Experience Platform kan het hosten van deze bestanden voor u beheren of u kunt het zelf doen.

## Beheerd door Adobe {#managed-by-adobe}

Adobe is niet bezig met webhosting. Als u ervoor kiest om Adobe de hosting te laten beheren, worden uw builds geleverd aan een netwerk van de derdeinhoudslevering (CDN) waarmee wij een contract hebben.

Momenteel is de primaire CDN-provider Akamai. Bestanden die op Akamai worden gehost, hebben het domein `assets.adobedtm.com` .

### Waarom beheerde hosting gebruiken?

De belangrijkste reden om beheerde hosting te gebruiken is gemak. Het is eenvoudiger om de vereiste host te maken en u hoeft zich geen zorgen te maken over onderhoud.

## Zelfhosting

Als u niet wilt dat Adobe uw gehoste bestanden beheert, moet u deze zelf hosten. Als u uw bestanden wilt hosten, moet u de voltooide builds van Experience Platform ophalen en ervoor zorgen dat de bestanden via de releasecyclus van uw bedrijf op door het bedrijf beheerde servers worden geplaatst.

### Waarom zelfhosting gebruiken?

Er zijn een aantal redenen om ervoor te kiezen om uw eigen build-bestanden te hosten.

* Sommige browsers blokkeren het assets.adobedtm.com domein op de privacymontages wordt gebaseerd de eindgebruiker heeft gevormd
* Zelf-ontvangen vermindert het vereiste aantal DNS raadplegingen
* U hebt specifieke kopteksten u voor veiligheid moet plaatsen
* De vereisten voor het beheren van de cache verschillen van de standaardinstellingen van Adobe
* U wilt meer controle over de locatie van de randknooppunten
* Uw organisatie heeft veiligheids- en wettelijke vereisten die u verhinderen de door Adobe beheerde optie te gebruiken

### Hoe te zelf-gastheer

Er zijn twee methodes u kunt gebruiken om voltooide bouwstijlen te verwerven zodat u zelf-gastheer kunt.

* Downloaden
* Directe levering

#### Downloaden

De builds kunnen worden geleverd als een gecomprimeerd ZIP-bestand (codering optioneel). Vervolgens kunt u het pakket uitpakken en de inhoud in uw releasecyclus invoegen en deze op uw eigen servers plaatsen.

Gebruik a [&#x200B; die door de gastheer van Adobe &#x200B;](self-hosting-libraries.md) wordt beheerd en selecteer de [&#x200B; optie van het Archief &#x200B;](../environments.md) op uw milieu. De omgeving biedt een downloadkoppeling. Wanneer een build wordt gemaakt, kunt u deze ophalen via de downloadkoppeling van de omgeving.

#### Directe levering

De builds kunnen ook rechtstreeks aan een server worden geleverd SFTP die u creeerde. U neemt de verantwoordelijkheid om deze gegevens in uw releasecyclus in te voeren en ze live te zetten.

Om een directe levering uit te voeren, zou u een [&#x200B; gastheer van SFTP &#x200B;](sftp-host.md) moeten creëren en die gastheer aan uw milieu toewijzen. Wanneer u in die omgeving een bibliotheek maakt, worden de bestanden geleverd aan uw SFTP-server.
