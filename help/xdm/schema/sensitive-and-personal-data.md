---
title: Gevoelige en Persoonlijke Informatie in XDM
description: Leer over zeer belangrijke overwegingen betreffende gevoelige persoonlijke informatie (SPI) en persoonlijk identificeerbare informatie (PII) in het Model van de Gegevens van de Ervaring (XDM).
source-git-commit: 76815389a1c87fbf908e499c50594a4b356a11a9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Gevoelige en persoonlijke informatie in XDM

Het Model van Gegevens van de ervaring (XDM) verstrekt standaardgegevensstructuren voor gebruik in Adobe Experience Platform, die u toestaan om gegevens over klantenervaringen te verzamelen. Deze gegevens kunnen gevoelige persoonlijke informatie (SPI) en persoonlijk identificeerbare informatie (PII) zoals het e-mailadres, de naam, de rekening ID, en andere gegevensgebieden van een klant omvatten.

Organisatieregels en wettelijke privacyregels zoals de algemene gegevensbeschermingsverordening (GDPR) dwingen beperkingen af op de manier waarop SPI en PII kunnen worden verzameld, opgeslagen, gebruikt en gedeeld. Daarom is het belangrijk om te overwegen welke gebieden gevoelige of persoonlijke informatie in uw gegevensmodel vertegenwoordigen en ervoor te zorgen dat uw verrichtingen binnen organisatorische en wettelijke richtlijnen vallen.

Dit document behandelt belangrijke overwegingen betreffende gevoelige en persoonlijke gegevens in XDM.

## Bepalen welke velden gevoelige of persoonlijke gegevens bevatten

Wat SPI en PII vormt is zeer contextspecifiek, en het is daarom aan u om uw gegevensmodel, bedrijfsverrichtingen, en toepasselijke verordeningen te begrijpen om te bepalen welke schemagebieden gevoelige of persoonlijke gegevens vertegenwoordigen.

De juridische jurisdictie van uw klanten heeft bijvoorbeeld een rechtstreeks effect op welke informatie als gevoelig wordt beschouwd. De GDPR biedt robuuste definities voor SPI en PII, maar klanten buiten de Europese Economische Ruimte (EER) kunnen aan verschillende definities en beperkingen worden onderworpen.

## Behandeling van gevoelige en persoonlijke gegevens

Net als de definities voor gevoelige en persoonsgegevens zelf zijn de beperkingen voor de verwerking van deze gegevens ook contextspecifiek.

De instemming van de klant is vaak een kritieke factor in termen van welke gegevens kunnen worden verzameld en verwerkt, en voor welke doeleinden. Afhankelijk van de rechtsbevoegdheid waaronder uw klanten vallen, kan uitdrukkelijke toestemming vereist zijn om hun gevoelige en persoonlijke gegevens te verzamelen. Zelfs in gevallen waarin uitdrukkelijke toestemming niet vereist is, zijn beperkingen voor gegevensverwerking nog steeds van toepassing, afhankelijk van wat de privacyverklaring aan de klant zegt.

Raadpleeg uw juridische team om te bepalen hoe vertrouwelijke en persoonlijke gegevens moeten worden verwerkt voor uw zaken die u gebruikt.

## Beperking van het gebruik van gevoelige en persoonsgegevens

XDM verstrekt een verscheidenheid van standaardgebiedsgroepen en gegevenstypes om relevante, algemeen gebruikte gegevensstructuren te beschrijven om klantenervaringen te aandrijven. Als een geadviseerde standaardmiddel beperkte gebieden bevat die u niet in uw schema&#39;s wilt omvatten, nochtans, moet u dat middel niet gebruiken.

Met Platform kunt u uw eigen aangepaste veldgroepen en gegevenstypen definiëren, zodat u volledig zelf kunt bepalen hoe uw gegevens zijn gestructureerd als beschikbare standaardbronnen niet aan uw behoeften voldoen. Raadpleeg de volgende documentatie voor meer informatie over het definiëren van deze aangepaste bronnen:

* [Een aangepaste veldgroep maken](../ui/resources/field-groups.md#create)
* [Een aangepast gegevenstype maken](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## Volgende stappen

Dit document behandelde zeer belangrijke overwegingen betreffende gevoelige en persoonlijke gegevens in XDM. Voor meer informatie over hoe te om uw schema&#39;s te modelleren om uw zaken van het bedrijfsgebruik het best te ontmoeten, verwijs naar de gids op [best practices voor gegevensmodellering](./best-practices.md).

Voor meer informatie, gegevensbeheer en privacy mogelijkheden in Experience Platform, zie het overzicht over [bestuur, privacy en veiligheid](../../landing/governance-privacy-security/overview.md).
