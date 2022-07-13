---
title: Ondersteuning voor aflopen van tags in Internet Explorer 10 en 11
description: Adobe Experience Platform biedt geen ondersteuning meer voor updates voor tags in Internet Explorer 10 en 11.
source-git-commit: 0103f1af37dc202087d3c81d495de88d3de7c377
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Ondersteuning voor eindtags in Internet Explorer 10 en 11

Aangezien het landschap van de online digitale ervaring blijft evolueren, investeert Adobe niet meer middelen om Internet Explorer 10 (IE10) en Internet Explorer 11 (IE11) voor markeringen in Adobe Experience Platform te steunen. Hoewel Adobe de ondersteuning voor IE10 en IE11 niet actief verwijdert, wordt het effect van deze browsers op nieuwe functies niet langer in overweging genomen in toekomstige updates.

## Waarom worden IE10 en IE11 niet meer ondersteund?

Er zijn vier redenen waarom tags geen ondersteuning meer bieden voor IE10 en IE11:

* **Microsoft beëindigt de steun voor IE10 en IE11**: Vanaf januari 2020 [Microsoft biedt geen ondersteuning voor IE10](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-10-end-of-support) voor beveiligings- en niet-beveiligingsupdates. Vanaf juni 2022 [Microsoft biedt geen ondersteuning voor IE11](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-11-end-of-support) in bepaalde versies van Windows.
* **De bredere industrie staakt de steun van IE10 en IE11**: Naarmate de industrie minder ondersteuning biedt voor IE10 en IE11, wordt de mogelijkheid voor tags om achterwaartse compatibiliteit met deze technologieën te behouden steeds meer gehinderd.
* **Moderne technologieën bieden geen ondersteuning voor IE10 en IE11**: Als tags de modernste technologieën moeten blijven ondersteunen, moet IE10 en IE11 niet meer worden ondersteund omdat deze moderne technologieën niet compatibel zijn met deze webbrowsers.
* **Ondersteuning voor IE10 en IE11 vertraagt de algemene ontwikkeling van functies**: Voor veel nieuwe functies die voor tags worden vrijgegeven, moet u zorgvuldig rekening houden met IE10 en IE11. Deze overweging resulteert in uren extra werk om moeilijk te vinden testende hulpmiddelen te verwerven die met IE10 en IE11 werken, extra code toevoegen om eigenschappen te maken werken met IE10 en IE11 die geen inheemse steun hebben, en onderzoek om ervoor te zorgen de eigenschap zoals verwacht werkt. Door de ondersteuning voor IE10 en IE11 stop te zetten, kan Adobe sneller nieuwe functies leveren.

## Effecten van IE10- en IE11-afleiding

Nadat de ondersteuning is afgekeurd, vinden de volgende effecten plaats:

* Nieuwe functies bieden mogelijk geen ondersteuning voor IE10 en IE11.
* Het testen op huidige en nieuwe functieondersteuning met IE10 en IE11 wordt stopgezet.
* Functies die ooit door IE10 en IE11 werden ondersteund, ondersteunen deze browsers mogelijk niet meer.
