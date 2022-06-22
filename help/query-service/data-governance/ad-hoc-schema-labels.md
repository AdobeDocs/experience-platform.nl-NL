---
title: Op kenmerken gebaseerde ondersteuning voor toegangsbeheer voor ad-hocschema's
description: Een handleiding voor het beperken van toegang tot gegevensvelden in ad-hocschema's die via Adobe Experience Platform Query Service worden gegenereerd.
source-git-commit: 3d908face315c7aa2ad8f6350fb1fe0d3446d428
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# Op kenmerken gebaseerde ondersteuning voor toegangsbeheer voor ad-hocschema&#39;s

Gegevens die naar Adobe Experience Platform worden overgebracht, worden ingekapseld door XDM-schema&#39;s (Experience Data Model) en kunnen onderworpen zijn aan gebruiksbeperkingen die door uw organisatie of wettelijke voorschriften zijn gedefinieerd.

Door een vraag CTAS door de Dienst van de Vraag uit te voeren wanneer geen schema wordt gespecificeerd, wordt een ad hoc schema automatisch geproduceerd. Het is vaak noodzakelijk het gebruik van bepaalde velden, of gegevensreeksen, van ad-hocregelingen te beperken om de toegang tot zowel gevoelige persoonsgegevens als persoonlijk identificeerbare informatie te controleren. Adobe Experience Platform vergemakkelijkt dit toegangsbeheer door u toe te staan om schemagebieden door het Platform UI te etiketteren gebruikend het op attribuut-gebaseerde toegangsbeheervermogen.

Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. Hoewel, is het beste praktijken om gegevens te etiketteren zodra het in Platform wordt opgenomen, of zodra de gegevens voor gebruik in Platform beschikbaar worden.

Het op schema-gebaseerde etiketteren is een belangrijke component van op attribuut-gebaseerde toegangsbeheer om de toegang beter te beheren die aan gebruikers of groepen gebruikers wordt gegeven. Met Adobe Experience Platform kunt u de toegang tot elk veld in een ad-hocschema beperken door labels te maken en toe te passen.

Dit document biedt een zelfstudie om de toegang tot gevoelige gegevens te beheren door labels toe te passen op gegevensvelden van ad-hocschema&#39;s die via Query Service worden gegenereerd.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM-systeem (Experience Data Model)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html): Leer om schema&#39;s en andere middelen in de UI van het Platform tot stand te brengen en te beheren.
* [[!DNL Data Governance]](../../data-governance/home.md): Meer informatie [!DNL Data Governance] staat u toe om klantengegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren van toepassing op gegevensgebruik.
* [Op kenmerken gebaseerd toegangsbeheer](../../access-control/abac/overview.md): Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een ad-hocveld of een regulier schemaveld wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

## Een ad-hocschema maken

Zodra uw vraag is uitgevoerd en de resultaten zijn geproduceerd, wordt een ad hoc schema automatisch geproduceerd en toegevoegd aan de schemainventaris.

Als u een gegevenslabel wilt toevoegen, navigeert u naar [!UICONTROL Schemas] het dashboard bladert lusje door te selecteren [!UICONTROL Schemas] in de linkerspoorstaaf van de gebruikersinterface van het Platform. Het schema-overzicht wordt weergegeven.

>[!NOTE]
>
>Ad hoc schema&#39;s worden niet door gebrek getoond in de schemainventaris.

## Ontdek ad-hocschema&#39;s in de schemainventaris van de UI van het Platform

Als u de weergave van ad-hocschema&#39;s in de gebruikersinterface van het Platform wilt inschakelen, selecteert u het filterpictogram (../images/data-governance/filter.png) links van het zoekveld en selecteert u **[!UICONTROL Show adhoc schemas] in de linkerspoorstaaf die verschijnt.

![De opties voor het dashboardfilter van het Schema laten spoor met de schakeloptie &#39;Ad-hocschema tonen&#39; ingeschakeld.](../images/data-governance/adhoc-schema-toggle.png)

Selecteer de naam van het onlangs gemaakte ad-hocschema in de beschikbare lijst. Er wordt een visualisatie van de structuur van het ad-hocschema weergegeven.

![Het voorbeeld ad hoc schemastructuurdiagram.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Regelgevingslabels bewerken

Als u gegevenslabels voor uw ad-hocschema wilt bewerken, selecteert u de optie [!UICONTROL Labels] tab. Met de werkruimte voor labels kunt u labels toepassen, maken en bewerken in uw ad-hocschemavelden en toegangsmachtigingen beheren via de gebruikersinterface. Alle velden in het ad-hocschema worden hier weergegeven.

## Labels voor het schema of veld bewerken

Als u de labels voor het hele schema wilt bewerken, selecteert u het potloodpictogram (![](../images/data-governance/edit-icon.png)) aan de zijkant van de naam van het schema onder de [!UICONTROL Labels] tab.

![De labelweergave in de werkruimte Schema&#39;s met het potloodpictogram gemarkeerd.](../images/data-governance/edit-entire-schema-labels.png)

Als u een label op een bestaand veld wilt toepassen, selecteert u een of meer velden in de lijst gevolgd door [!UICONTROL Edit governance labels] in de rechterzijbalk.

![In de labelweergave in de werkruimte Schema&#39;s wordt de optie &#39;Regellabels bewerken&#39; gemarkeerd in het rechterzijpaneel.](../images/data-governance/edit-governance-labels.png)

## Pop-up Labels bewerken

De [!UICONTROL Edit labels] wordt weergegeven. Vanuit deze weergave kunt u bestaande governancelabels maken of bewerken via de gebruikersinterface.

![Het pop-upvenster met labels Bewerken.](../images/data-governance/edit-labels-popover.png)

Zie de documentatie voor richtlijnen over hoe u [labels maken of bewerken voor het geselecteerde schema of veld](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>Voor het maken van een nieuw label of het bewerken van een bestaand label zijn beheerdersmachtigingen voor uw organisatie vereist. Als u geen beheerdersrechten hebt, neemt u contact op met uw systeembeheerder om de toegang te regelen.

De etiketten kunnen ook worden gecreeerd gebruikend de toestemmingenwerkruimte. Zie de [handleiding voor het maken van labels in de werkruimte voor machtigingen](../../access-control/abac/ui/labels.md) voor instructies.

Zodra het aangewezen niveau van op attributen-gebaseerde toegangsbeheer is toegepast, is het volgende systeemgedrag op om het even welke vraag van toepassing die via de Dienst van de Vraag wordt uitgevoerd wanneer een gebruiker probeert om tot niet-toegankelijke gegevens toegang te hebben:

1. Als een gebruiker toegang tot één van de gebieden binnen een schema wordt geweigerd, zal de gebruiker niet op het beperkte gebied kunnen lezen of schrijven. Dit geldt voor de volgende algemene scenario&#39;s:

   * Wanneer een gebruiker een vraag met slechts een beperkte kolom probeert uit te voeren, zal het systeem een fout werpen dat de kolom niet bestaat.
   * Wanneer een gebruiker probeert om een vraag met veelvoudige kolommen uit te voeren die een beperkte kolom omvatten, zal het systeem output voor alle niet-beperkte slechts kolommen terugkeren.

1. Als een gebruiker om toegang tot een berekend gebied verzoekt, wordt de gebruiker vereist om toegang tot alle gebieden te hebben die in de samenstelling worden gebruikt of het systeem zal toegang tot het berekende gebied ontkennen.

Als een identiteit of primaire identiteit op ad hoc schema wordt geplaatst, neemt het systeem automatisch om het even welke bijbehorende verzoeken van de gegevenshygiëne in acht en ontruimt de gegevens in die datasets verbonden aan de identiteitskolom.

## Volgende stappen

Na het lezen van dit document hebt u een beter inzicht in hoe te om de etiketten van het gegevensgebruik aan ad hoc regelingen toe te voegen die door de vragen van de Dienst CTAS van de Vraag worden gecreeerd. Als u dit nog niet hebt gedaan, zijn de volgende documenten nuttig om uw inzicht in gegevensbeheer in de Dienst van de Vraag te verbeteren:

* [Identiteiten ad-hocschema](./ad-hoc-schema-identities.md)
* [Gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)
