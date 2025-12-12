---
title: Ondersteuning voor Subresource Integrity (SRI)
description: Leer hoe de integriteit van het submiddel (SRI) in Adobe Experience Platform wordt gesteund.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Ondersteuning voor Subresource Integrity (SRI)

Dit document behandelt hoe de integriteit van subresources (SRI) in Adobe Experience Platform wordt gesteund.

Moderne websites worden samengesteld door te verwijzen naar afbeeldingen, inhoud en scripts van verschillende locaties op het web. SRI staat browser toe om te verifiëren dat de inhoud van een gevraagd dossier niet onverwacht is gewijzigd.

Terwijl hun gebruiksgevallen elkaar aanvullen, is SRI verschillend van een Beleid van de Veiligheid van de Inhoud (CSP), dat ervoor zorgt dat slechts dossiers van vertrouwde op bronnen op uw website worden toegestaan. SRI gaat één stap verder door ervoor te zorgen dat de inhoud van deze dossiers uw verwachtingen aanpast.

>[!NOTE]
>
>Voor meer gedetailleerde informatie over SRI, verwijs naar het [&#x200B; MDN Web docs &#x200B;](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity).

Het SRI-validatieproces kan als volgt worden samengevat:

1. U genereert een cryptografische hash van het element dat u wilt valideren.
1. Op uw website wordt de hash geplaatst in het `integrity` -kenmerk van het HTML-element dat het bestand laadt.
1. Wanneer de browser het kenmerk `integrity` ziet, vraagt de browser om de bron en genereert deze onafhankelijk een eigen versie van de cryptografische hash.
1. De browser vergelijkt de hash van `integrity` met de hash die deze heeft gegenereerd. Als ze overeenkomen, is het element toegestaan. Als ze niet overeenkomen, wordt het middel geblokkeerd.

## Beperkingen in systemen voor tagbeheer

Als TMS-systeem (Tag-Management System) bieden tags in Adobe Experience Platform een gecompileerde JavaScript-bibliotheekbuild die u met één `<script>` -element (Embed-code) op uw pagina&#39;s laadt. De dynamische functionaliteit die door TMS wordt verleend wordt verwezenlijkt door de inhoud van dat manuscript dynamisch uit te ruilen zonder u te vereisen om iets anders te veranderen.

Wanneer de inhoud van het script verandert, verandert de cryptografische hash van deze inhoud. Daarom is de enige manier om SRI met TMS te maken werken door uw ingebedde code tezelfdertijd bij te werken dat u een nieuwe bouwstijl publiceert. Voor velen is dit in de eerste plaats het doel van het gebruik van een TMS.

De volgende beste beveiligingsoptie voor tags is het implementeren van een Content Security Policy. Voor meer informatie, zie de gids op [&#x200B; CSPs en markeringen &#x200B;](./content-security-policy.md).

## SRI integreren in build-implementatie

Als u nog SRI voor uw bibliotheekbouwstijlen wilt gebruiken, moet u zelf-ontvangen gebruiken. Als u het ontvangen van Adobe-Beheerde gebruikt, is er geen manier om SRI te gebruiken zonder enige hoeveelheid tijd te hebben waar de nieuwe bouwstijlinhoud niet het `integrity` attribuut van inbedcode aanpast.

Het automatiseren van het bijwerken van uw insluitcode varieert afhankelijk van de structuur van uw site, maar de algemene stappen kunnen als volgt worden samengevat:

1. Haal de build van de productiebibliotheek op via SFTP-levering of door het archief te downloaden vanuit de gebruikersinterface.
1. Genereer de cryptografische hash van de hoofdbuild.
1. Zorg ervoor dat het kenmerk `integrity` van de insluitcode wordt bijgewerkt naar de nieuwe hash en dat de build waarnaar wordt verwezen, wordt bijgewerkt als onderdeel van dezelfde implementatie.

>[!IMPORTANT]
>
>Deze aanpak heeft alleen betrekking op de belangrijkste bouwsteen. Het omvat geen van de kleinere dossiers die kunnen bestaan.

## Volgende stappen

Dit document behandelde de beperkingen om SRI met markeringen te gebruiken, en de stappen die worden vereist om het in uw bibliotheek te integreren bouwt plaatsingen ondanks die beperkingen. Als u niet reeds hebt, wordt het sterk geadviseerd dat u de gids op [&#x200B; CSPs en markeringen &#x200B;](./content-security-policy.md) voor een alternatieve veiligheidsoptie leest.
