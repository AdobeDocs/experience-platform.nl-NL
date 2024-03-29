---
title: Ondersteuning voor Subresource Integrity (SRI)
description: Leer hoe de integriteit van het submiddel (SRI) in Adobe Experience Platform wordt gesteund.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Ondersteuning voor Subresource Integrity (SRI)

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Dit document behandelt hoe de integriteit van subresources (SRI) in Adobe Experience Platform wordt gesteund.

Moderne websites worden samengesteld door te verwijzen naar afbeeldingen, inhoud en scripts van verschillende locaties op het web. SRI staat browser toe om te verifiëren dat de inhoud van een gevraagd dossier niet onverwacht is gewijzigd.

Terwijl hun gebruiksgevallen elkaar aanvullen, is SRI verschillend van een Beleid van de Veiligheid van de Inhoud (CSP), dat ervoor zorgt dat slechts dossiers van vertrouwde op bronnen op uw website worden toegestaan. SRI gaat één stap verder door ervoor te zorgen dat de inhoud van deze dossiers uw verwachtingen aanpast.

>[!NOTE]
>
>Voor meer gedetailleerde informatie over SRI, verwijs naar [MDN-webdocumenten](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity).

Het SRI-validatieproces kan als volgt worden samengevat:

1. U genereert een cryptografische hash van het element dat u wilt valideren.
1. Op uw website wordt de hash in het dialoogvenster `integrity` kenmerk van het element HTML dat het bestand laadt.
1. Wanneer de browser de `integrity` , vraagt de browser de bron op en genereert onafhankelijk een eigen versie van de cryptografische hash.
1. De browser vergelijkt de `integrity` hash met de ontstane hash. Als ze overeenkomen, is het element toegestaan. Als ze niet overeenkomen, wordt het middel geblokkeerd.

## Beperkingen in systemen voor tagbeheer

Als TMS-systeem (tag-management system) bieden tags in Adobe Experience Platform een gecompileerde JavaScript-bibliotheekbuild die u op uw pagina&#39;s laadt met één enkele `<script>` element (code insluiten). De dynamische functionaliteit die door TMS wordt verleend wordt verwezenlijkt door de inhoud van dat manuscript dynamisch uit te ruilen zonder u te vereisen om iets anders te veranderen.

Wanneer de inhoud van het script verandert, verandert de cryptografische hash van deze inhoud. Daarom is de enige manier om SRI met TMS te maken werken door uw ingebedde code tezelfdertijd bij te werken dat u een nieuwe bouwstijl publiceert. Voor velen is dit in de eerste plaats het doel van het gebruik van een TMS.

De volgende beste veiligheidsoptie voor markeringen is een Beleid van de Veiligheid van de Inhoud uit te voeren. Zie de handleiding voor meer informatie over [CSP&#39;s en codes](./content-security-policy.md).

## SRI integreren in build-implementatie

Als u nog SRI voor uw bibliotheekbouwstijlen wilt gebruiken, moet u zelf-ontvangen gebruiken. Als u Adobe-geleide het ontvangen gebruikt, is er geen manier om SRI te gebruiken zonder enige hoeveelheid tijd te hebben waar de nieuwe bouwstijlinhoud niet aanpast `integrity` kenmerk van de insluitcode.

Het automatiseren van het bijwerken van uw insluitcode varieert afhankelijk van de structuur van uw site, maar de algemene stappen kunnen als volgt worden samengevat:

1. Haal de build van de productiebibliotheek op via SFTP-levering of door het archief te downloaden vanuit de gebruikersinterface.
1. Genereer de cryptografische hash van de hoofdbuild.
1. Zorg ervoor dat de insluitcode `integrity` attribuut wordt bijgewerkt aan de nieuwe knoeiboel, en dat referenced bouwstijl als deel van de zelfde plaatsing wordt bijgewerkt.

>[!IMPORTANT]
>
>Deze aanpak heeft alleen betrekking op de belangrijkste bouwsteen. Het omvat geen van de kleinere dossiers die kunnen bestaan.

## Volgende stappen

Dit document behandelde de beperkingen om SRI met markeringen te gebruiken, en de stappen die worden vereist om het in uw bibliotheek te integreren bouwt plaatsingen ondanks die beperkingen. Als u dit nog niet hebt gedaan, is het sterk aan te raden de handleiding te lezen op [CSP&#39;s en codes](./content-security-policy.md) voor een andere beveiligingsoptie.
