---
keywords: Experience Platform;home;popular topics;namespace;Namespace;Namespaces;namespaces;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: 'Identiteitsnaamruimten zijn een onderdeel van Identiteitsdienst dat fungeert als indicator van de context waarop een identiteit betrekking heeft. Ze onderscheiden bijvoorbeeld de waarde "name@email.com" als e-mailadres of "443522" als een numerieke CRM-id. '
translation-type: tm+mt
source-git-commit: dfb16c1808ac61e6c4f4d97c08ac3d1dcc8499a8
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 1%

---


# Overzicht naamruimte identiteit

Identiteitsnaamruimten zijn een component van [[!DNL Identity Service]](./home.md) die dienen als indicatoren van de context waarop een identiteit betrekking heeft. Ze onderscheiden bijvoorbeeld de waarde &quot;name<span>@email.com&quot; als e-mailadres of &quot;443522&quot; als een numerieke CRM-id.

## Aan de slag

Als u met naamruimten werkt, moet u de verschillende betrokken Adobe Experience Platform-services begrijpen. Voordat u begint te werken met naamruimten, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Identity Service]](./home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
- [[!DNL Privacy Service]](../privacy-service/home.md): Identiteitsnaamruimten worden gebruikt om te voldoen aan de algemene gegevensbeschermingsverordening (GDPR), waarbij GDPR-aanvragen kunnen worden ingediend ten opzichte van een naamruimte.

## Naamruimten voor identiteiten

Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace. Bij het afstemmen van recordgegevens over profielfragmenten, zoals bij het [!DNL Real-time Customer Profile] samenvoegen van profielgegevens, moeten zowel de identiteitswaarde als de naamruimte overeenkomen.

Twee profielfragmenten kunnen bijvoorbeeld verschillende primaire id&#39;s bevatten, maar ze hebben dezelfde waarde voor de naamruimte E-mail, zodat Platform kan zien dat deze fragmenten in feite dezelfde persoon zijn en de gegevens samenbrengt in de identiteitsgrafiek voor de persoon.

![](images/identity-service-stitching.png)

### Identiteitstypen

Gegevens kunnen worden geïdentificeerd door verschillende typen identiteiten. Het identiteitstype wordt gespecificeerd op het tijdstip dat identiteitskaart namespace wordt gecreeerd en controleert al dan niet het gegeven aan de identiteitsgrafiek en om het even welke speciale instructies voor hoe die gegevens zouden moeten worden behandeld wordt voortgeduurd.

De volgende identiteitstypen zijn beschikbaar binnen [!DNL Platform]:

| Identiteitstype | Beschrijving |
| --- | --- |
| Cookie | Deze identiteiten zijn essentieel voor uitbreiding en vormen het grootste deel van de identiteitsgrafiek. Maar door de natuur verval ze snel en verliezen hun waarde in de loop der tijd. Verwijderen van cookies wordt speciaal verwerkt in de identiteitsgrafiek. |
| Cross-device | Dit geeft aan dat dit als een sterke personele identificator [!DNL Identity Service] moet worden beschouwd en dus voor altijd moet worden bewaard. Voorbeelden zijn een aanmeldings-id, CRM-id, loyaliteitsidentiteitskaart enz. |
| Apparaat | Omvat IDFA, GAID en andere IOT-id&#39;s. Deze kunnen door mensen in huishoudens worden gedeeld. |
| Email | Tot dit type identiteiten behoren ook PII&#39;s (Persoonlijke identificeerbare informatie). Dit is een aanwijzing om de waarde gevoelig [!DNL Identity Service] te verwerken. |
| Mobile | Tot dit type identiteiten behoren PII. Dit is een aanwijzing om de waarde gevoelig [!DNL Identity Service] te verwerken. |
| Niet-personen | Wordt gebruikt voor het opslaan van id&#39;s die naamruimten nodig hebben, maar die niet zijn gekoppeld aan een personencluster. Deze id&#39;s worden vervolgens gefilterd uit de identiteitsgrafiek. Mogelijke gebruiksgevallen zijn onder meer gegevens over producten, organisaties, winkels, enz. (Bijvoorbeeld een product-SKU.) |
| Telefoon | Tot dit type identiteiten behoren PII. Dit is een aanwijzing om de waarde gevoelig [!DNL Identity Service] te behandelen. |

### Standaardnaamruimten {#standard}

Adobe Experience Platform biedt verschillende naamruimten die beschikbaar zijn voor alle organisaties. Deze worden standaardnaamruimten genoemd en zijn zichtbaar met de [!DNL Identity Service] API of via de [!DNL Platform] interface.

Als u de standaardnaamruimten in de gebruikersinterface wilt weergeven, klikt u op **[!UICONTROL Identiteiten]** in de linkertrack en klikt u vervolgens op het tabblad **[!UICONTROL Bladeren]** . Alle naamruimten die voor uw organisatie toegankelijk zijn, worden weergegeven. De naamruimten met &quot;[!UICONTROL Standaard]&quot; als &quot;[!UICONTROL Eigenaar]&quot; zijn echter de standaardnaamruimten die door Adobe worden verschaft.

Vervolgens kunt u op een van de weergegeven naamruimten klikken om details weer te geven.

![](./images/standard-namespace-detail.png)

## Naamruimten beheren voor uw organisatie

Afhankelijk van uw organisatorische gegevens en gebruiksgevallen hebt u mogelijk aangepaste naamruimten nodig.

Deze worden in de gebruikersinterface weergegeven als naamruimten met &quot;[!UICONTROL Aangepast]&quot; als &quot;[!UICONTROL Eigenaar]&quot;. U kunt aangepaste naamruimten maken met de [!DNL Identity Service] API of via de gebruikersinterface.

Als u een aangepaste naamruimte wilt maken met de gebruikersinterface, klikt u op Naamruimte **** maken, vult u het dialoogvenster in en klikt u op **[!UICONTROL Maken]**.

De naamruimten die u definieert, zijn persoonlijk voor uw organisatie en hebben een uniek &#39;[!UICONTROL identiteitssymbool]&#39; (of &#39;code&#39; als u de API gebruikt) nodig om te kunnen worden gemaakt.

![](./images/create-identity-namespace.png)

Net als bij Standaard-naamruimten kunt u op een aangepaste naamruimte in het tabblad **[!UICONTROL Bladeren]** klikken om de details weer te geven. Met een aangepaste naamruimte kunt u echter ook de weergavenaam en -beschrijving van de naamruimte bewerken vanuit het detailgebied.

>[!NOTE]
>
>Nadat een naamruimte is gemaakt, kan deze niet worden verwijderd en kunnen de naamsymbolen (of de code in de API) en het type niet worden gewijzigd.

## Naamruimten in identiteitsgegevens

Het leveren van de naamruimte voor een identiteit is afhankelijk van de methode die u gebruikt voor het opgeven van identiteitsgegevens. Zie de sectie over het [verstrekken van identiteitsgegevens](./home.md#supplying-identity-data-to-identity-service) in het [!DNL Identity Service] overzicht voor meer informatie over het verstrekken van identiteitsgegevens.
