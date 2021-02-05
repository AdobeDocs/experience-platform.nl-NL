---
keywords: identities rtcdp;rtcdp-identiteiten;real-time cdp-identiteiten
title: Identiteiten in Real-time Platform van de Gegevens van de Klant
description: Met de Adobe Experience Platform Identity Service kunt u uw klanten en hun gedrag beter zien door identiteiten tussen apparaten en systemen te combineren.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# Identiteiten in Real-time Platform van de Gegevens van de Klant

Met Adobe Experience Platform [!DNL Identity Service] kunt u uw klanten en hun gedrag beter zien door identiteiten tussen apparaten en systemen te combineren. Doorgaans communiceren uw klanten via meerdere kanalen met uw merk. U kunt onder andere online door uw website bladeren, een aankoop in de winkel doen, deelnemen aan uw loyaliteitsprogramma of een helpdesk bellen voor ondersteuning, om er een paar te noemen. In deze verschillende systemen is er een identiteit gemaakt voor die klant en met [!DNL Identity Service] kunnen deze identiteiten worden samengebracht om het volledige beeld te zien.

Nu, in plaats van vijf afzonderlijke klanten die met uw merk over vijf verschillende kanalen in wisselwerking staan, kunt u zien dat dit de zelfde klant is, en u kunt ervoor zorgen zij een verenigbare, gepersonaliseerde, relevante ervaring door elke interactie ontvangen. Naarmate meer informatie bekend raakt over uw klant (bijvoorbeeld een anonieme browser van uw website besluit zich aan te melden voor een account en zich aan te melden), wordt deze informatie aan elkaar gekoppeld en wordt het beeld van uw klant steeds duidelijker.

## Identiteitsnaamruimten

Identiteitsnaamruimten zijn een onderdeel van [!DNL Identity Service] en dienen als indicatoren die aanvullende context bieden aan de identiteit van de klant. Een voorbeeld van een veelgebruikte naamruimte voor id is &#39;E-mail&#39;, waarbij u met hetzelfde e-mailadres voor meerdere websites verschillende identiteiten kunt samenvoegen, elk met een unieke klant-id, zoals u eigenlijk bij dezelfde klant hoort. [!DNL Experience Platform] kunt u id-naamruimten gebruiken om te zoeken naar afzonderlijke profielen in de gebruikersinterface. Zie het [overzicht van de profielviewer](/help/rtcdp/profile/profile-viewer.md) voor meer informatie over het weergeven van profielen. Voor meer informatie over identiteitsnaamruimten, zie [identity namespace overzicht](../../identity-service/namespaces.md).

## Identiteitsgrafieken

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteitsnamespaces, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat. Alle identiteitsgrafieken van klanten worden gezamenlijk beheerd en bijgewerkt door [!DNL Identity Service] in bijna real-time, als reactie op klantactiviteiten.

[!DNL Identity Service] beheert een identiteitsgrafiek zichtbaar door slechts uw organisatie en gebouwd die op uw gegevens wordt gebouwd, die als privé grafiek wordt bedoeld. [!DNL Identity Service] Hiermee vergroot u de persoonlijke grafiek wanneer een opgenomen gegevensrecord meer dan één identiteit bevat, waardoor een relatie tussen de gevonden identiteiten wordt toegevoegd.

## Volgende stappen

De identiteiten en de onderlinge relaties worden door [!DNL Identity Service] gedefinieerd en onderhouden en door [!DNL Real-time Customer Profile] gebruikt om een volledig beeld van elke individuele klant en zijn interacties te maken. Voor meer informatie raadpleegt u de [Identiteitsdocumentatie](../../identity-service/home.md).