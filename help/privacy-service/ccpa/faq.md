---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Veelgestelde vragen over CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---


# Veelgestelde vragen over CCPA

Dit document bevat antwoorden op veelgestelde vragen over de [!DNL California Consumer Protection Act] (CCPA) en de implementatie ervan in Adobe Experience Cloud.

## Wat is CCPA?

De [!DNL California Consumer Privacy Act] (CCPA) is de nieuwe privacywet van Californië die zijn inwoners nieuwe rechten met betrekking tot hun persoonlijke informatie verleent, en legt gegevensbeschermingstaken op aan bepaalde entiteiten die zaken in Californië leiden.

>[!NOTE]
>
>Hoewel dit technisch effectief is in januari 2020, wordt de CCPA nog steeds door de wetgevers verfijnd. Daarnaast zijn belangrijke implementatiedetails en andere informatie over richtlijnen opgenomen in regels die nog door de toezichthouder voor Californië moeten worden geschreven.

Hoewel de CCPA een aantal begrippen deelt die zijn opgenomen in de algemene verordening van de Europese Unie inzake gegevensbescherming (GDPR), zoals het recht van een individu op toegang tot en verwijdering van persoonlijke informatie, zijn er verschillende manieren waarop de CCPA van de GDPR verschilt. Zo biedt de CCPA consumenten een opt-out-recht voor bepaalde activiteiten inzake gegevensuitwisseling die als &quot;verkoop&quot; van persoonlijke informatie aan een derde worden aangemerkt, in plaats van voorafgaande toestemming.

## Wat is de definitie van persoonlijke informatie in het kader van de CCPA?

Persoonlijke informatie is informatie &quot;die een consument of een huishouden identificeert, er verband mee houdt, beschrijft, daarmee in verband kan worden gebracht of redelijkerwijs direct of indirect aan een consument of een huishouden kan worden gekoppeld.&quot;

## Welke soorten persoonlijke gegevens of id&#39;s die in Adobe Experience Cloud worden gebruikt, zijn aan deze nieuwe vereisten onderworpen?

De volgende herkenningstekens worden algemeen gebruikt in [!DNL Experience Cloud] toepassingen en zouden aan vereisten kunnen onderworpen zijn CCPA:

- Naam
- Postadres
- Unieke persoonlijke identificatiecode
- Online-id
- IP-adres
- E-mailadres
- Accountnaam

Persoonlijke informatie kan ook informatie over internet of andere elektronische netwerkactiviteiten bevatten. Dit omvat onder meer, maar is niet beperkt tot:

- Browsergeschiedenis
- Zoekgeschiedenis
- Informatie over de interactie van een consument met een website, toepassing of advertentie

Hoewel CCPA een groot aantal persoonlijke gegevens bestrijkt, wordt in de standaardcontractvoorwaarden van Adobe bepaald dat gevoelige persoonlijke gegevens (zoals SSN, informatie over rijbewijzen, informatie over financiële rekeningen en biometrische gegevens) over het algemeen niet mogen worden geïmporteerd en gebruikt in [!DNL Experience Cloud] toepassingen.

## Op welke wijze zijn de verschillende rollen en verantwoordelijkheden van de CCPA van toepassing [!DNL Experience Cloud]?

Zoals bepaald door CCPA, zijn de volgende rollen op Adobe en zijn klanten van toepassing:

- Adobe-klanten (de partij die de verzameling en het gebruik van persoonlijke gegevens van ingezetenen van Californië aanvraagt) worden beschouwd als een **bedrijf**.
- Adobe zou in zijn rol van het verlenen van de dienst, als een **Dienstverlener** worden beschouwd.

Gezien deze relatie en de contracttaal van Adobe, zou openbaarmaking aan Adobe waarschijnlijk niet worden beschouwd als een &quot;verkoop&quot; waarvoor bedrijven kennisgeving moeten doen en een opt-out moeten aanbieden.

Adobe-services kunnen echter worden gebruikt om bepaalde gegevens te delen en over te dragen aan derden. Deze overdrachten door derden kunnen worden beschouwd als een &quot;verkoop&quot; en vereisen wettelijk openbaarmaking en opt-out.  Klanten moeten met hun juridische adviseur samenwerken om specifieke gebruiksgevallen te evalueren om toepasselijke vereisten te beoordelen.

## Hoeveel dagen moet een bedrijf reageren op een verzoek van de consument om toegang te krijgen tot of persoonlijke informatie te verwijderen?

Ervan uitgaande dat de zaken persoonlijke informatie hebben verzameld en dat het de identiteit van een bepaalde consument van Californië voor authentiek kan verklaren of verifiëren, staat CCPA voor consumentenverzoeken toe om binnen 45 dagen (met sommige uitzonderingen) worden voldaan.

## Wat is de rol van Adobe onder CCPA?

Als Serviceverlener verzamelt en verwerkt Adobe persoonlijke gegevens namens het bedrijf en is contractueel gebonden deze gegevens alleen te gebruiken voor de specifieke doeleinden die in de overeenkomst zijn vermeld.

Gezien deze relatie en de contracttaal van Adobe, vallen openbaarmakingen aan Adobe binnen de wettelijke bepalingen voor Dienstverleners, en waarschijnlijk niet als &quot;verkoop&quot;worden beschouwd waarvoor de ondernemingen bericht zouden moeten verstrekken en een opt-out zouden moeten aanbieden.

Adobe-services kunnen worden gebruikt om bepaalde gegevens te delen en over te dragen aan derden. Deze overdrachten door derden kunnen worden beschouwd als een &quot;verkoop&quot; en vereisen wettelijk openbaarmaking en opt-out.  Klanten moeten met hun juridische adviseur samenwerken om specifieke gebruiksgevallen te evalueren om toepasselijke vereisten te beoordelen.

## Hoe kan ik de privacyvereisten voor consumenten in het kader van de CCPA ondersteunen als ik bepaalde soorten gegevens handhaaf die onder de vereisten vallen?

Zodra u de noodzakelijke stappen hebt genomen om consumenten van CA voor authentiek te verklaren, [!DNL Privacy Service] staat het Adobe Experience Platform u toe om de privacyverzoeken van de consument aan compatibele [!DNL Experience Cloud] toepassingen voor te leggen. Zie het overzicht [van de](../home.md) Privacy Service voor meer informatie. Raadpleeg de handleiding over [!DNL Experience Cloud] Privacy Service- en Experience Cloud-toepassingen [voor meer informatie over hoe uw specifieke](../experience-cloud-apps.md)toepassingen aan uw privacyverzoeken kunnen voldoen.

>[!NOTE]
>
>De toezichthouder van Californië hanteert nog steeds nadere aanwijzingen over de soorten gegevens die in aanmerking komen voor privacyverzoeken van consumenten.

## Biedt Adobe andere hulpmiddelen aan die nuttig kunnen zijn in het richten van vereisten CCPA?

Adobe Experience Cloud-toepassingen bieden functies voor gegevensbeheer en -beheer die van nut kunnen zijn voor de privacybehoeften van bedrijven. Onder deze hulpmiddelen zijn het etiketteren van het gegevensgebruik, op rol-gebaseerde toegangscontroles, IP obfuscation, en het hakken mogelijkheden.

Adobe heeft diverse certificeringen ontvangen van zijn privacy- en beveiligingspraktijken, zoals een ISO 27001-certificering en een TrustArc GDPR-validatie.