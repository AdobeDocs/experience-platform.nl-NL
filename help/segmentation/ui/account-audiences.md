---
title: Accountsoorten
description: Leer hoe u accountpubliek kunt maken en gebruiken om accountprofielen in downstreamdoelen te gebruiken.
badgeLimitedAvailability: label="Beperkte beschikbaarheid" type="Caution"
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 1ff4cb004b7c2f474e2d64f4bcc239c7060f9439
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---

# Accountpubliek

>[!AVAILABILITY]
>
>Accountpubliek is alleen beschikbaar in het dialoogvenster [B2B Edition van Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). Bovendien is de functionaliteit voor het accountpubliek momenteel in **beperkte beschikbaarheid**. Neem contact op met de klantenservice van de Adobe of uw Adobe om toegang tot deze functie te vragen.

Met de segmentatie van uw account kunt u in Adobe Experience Platform de volledige versnelling en verfijning van de segmentatieervaring van marketingmedewerkers van op mensen gebaseerde doelgroepen naar op account gebaseerde doelgroepen brengen.

Accountpubliek kan worden gebruikt als input voor op account gebaseerde bestemmingen, zodat u zich kunt richten op de personen binnen die accounts in downstreamservices. U kunt bijvoorbeeld een publiek met een account gebruiken om records op te halen van alle accounts die dat wel doen **niet** beschikken over contactgegevens voor alle personen die de titel Chief Operating Officer (COO) of Chief Marketing Officer (CMO) hebben.

## Terminologie {#terminology}

Voordat u aan de slag gaat met het publiek van de account, bekijkt u eerst de verschillen tussen de verschillende soorten publiek:

- **Accountpubliek**: Een publiek in een account is een publiek dat is gemaakt met **account** profielgegevens. Accountprofielgegevens kunnen worden gebruikt om een publiek te maken dat zich richt op personen binnen downstreamaccounts. Lees voor meer informatie over accountprofielen de [overzicht van accountprofiel](../../rtcdp/accounts/account-profile-overview.md).
- **Personen**: Een publiek van een persoon is een publiek dat is gemaakt met **klant** profielgegevens. De profielgegevens van de klant kunnen worden gebruikt om publiek tot stand te brengen dat op de klantenkring van uw zaken gericht is. Lees voor meer informatie over klantprofielen de [Overzicht van het realtime klantprofiel](../../profile/home.md).
- **Doelgroepen**: Een publiek met perspectief is een publiek dat is gemaakt met **vooruitzicht** profielgegevens. Met profielgegevens kan een publiek van niet-geverifieerde gebruikers worden gemaakt. Lees voor meer informatie over perspectiefprofielen de [Overzicht van perspectiefprofielen](../../profile/ui/prospect-profile.md).

## Toegang {#access}

Als u toegang wilt tot het publiek van een account, selecteert u **[!UICONTROL Audiences]** in de **[!UICONTROL Accounts]** sectie.

![De knop Soorten publiek wordt gemarkeerd in de sectie Accounts.](../images/ui/account-audiences/select.png)

De [!UICONTROL Browse] wordt weergegeven en geeft een lijst weer van alle accountpubliek voor de organisatie.

![Het accountpubliek dat bij de organisatie hoort, wordt weergegeven.](../images/ui/account-audiences/browse.png)

Deze weergave bevat informatie over het publiek, zoals de naam, het aantal profielen, de oorsprong, de levenscyclusstatus, de datum waarop deze is gemaakt en de datum waarop deze voor het laatst is bijgewerkt.

## publiek maken {#create}

Als u een accountpubliek wilt maken, selecteert u **[!UICONTROL Create audience]** op de [!UICONTROL Browse] pagina.

![De [!UICONTROL Create audience] wordt gemarkeerd op de pagina waarop het publiek van de account bladert.](../images/ui/account-audiences/select-create-audience.png)

De Segment Builder wordt weergegeven. De accountkenmerken worden weergegeven op de linkernavigatiebalk.

![De Segment Builder wordt weergegeven. Merk op dat slechts de attributen worden getoond.](../images/ui/account-audiences/segment-builder.png)

Houd er rekening mee dat gebeurtenissen onder **[!UICONTROL People]**, in plaats van hun eigen tabblad te zijn, aangezien deze kenmerken aan personen zijn gekoppeld.

![De locatie waar naar gebeurtenissen moet worden gezocht, die zich binnen het [!UICONTROL People] wordt gemarkeerd.](../images/ui/account-audiences/attributes.png)

Voor meer informatie over het gebruik van de Segment Builder leest u de [Handleiding voor de gebruikersinterface van Segment Builder](./segment-builder.md).

## Het publiek activeren {#activate}

>[!NOTE]
>
>Slechts een beperkt aantal bestemmingen steunt rekeningspubliek. Zorg ervoor dat de bestemming die u wilt activeren, het accountpubliek ondersteunt voordat u doorgaat met dit proces.

Nadat u het publiek van uw account hebt gemaakt, kunt u het publiek activeren voor andere downstreamservices.

Selecteer het publiek dat u wilt activeren, gevolgd door **[!UICONTROL Activate to destination]**.

![De [!UICONTROL Activate to destination] wordt gemarkeerd in het menu met snelle acties voor het geselecteerde publiek.](../images/ui/account-audiences/activate.png)

De [!UICONTROL Activate destination] wordt weergegeven. Voor meer informatie over het activeringsproces, waaronder ondersteunde bestemmingen en meer informatie over veldtoewijzingen, leest u de [accountpubliek activeren](/help/destinations/ui/activate-account-audiences.md) zelfstudie.

## Volgende stappen {#next-steps}

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u uw accountpubliek kunt maken en gebruiken in Adobe Experience Platform. Als u wilt weten hoe u andere soorten publiek in Platform kunt gebruiken, leest u de [Handleiding voor segmentatieservice](./overview.md).

## Bijlage {#appendix}

In de volgende sectie vindt u aanvullende informatie over het accountpubliek.

### Validatie van accountsegmentatie {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Maximale fout in terugzoekvenster"
>abstract="Het maximale terugkijkvenster voor Experience Events is 30 dagen."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Maximale diepte van geneste container"
>abstract="De maximale diepte van geneste containers is **5**. Dit betekent dat u **kan** wanneer u een publiek maakt, hebt u meer dan vijf geneste containers."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Fout in maximumaantal regels"
>abstract="Het maximumaantal regels in één container is **5**. Dit betekent dat u **kan** wanneer u een publiek maakt, hebt u meer dan vijf regels in één container."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Fout in maximumbedrag van entiteit"
>abstract="Het maximumaantal entiteiten tussen verschillende entiteiten dat binnen één publiek kan worden gebruikt, is **5**. Een kruisentiteit is wanneer u tussen verschillende entiteiten in uw publiek verandert. Bijvoorbeeld, ga van een Rekening naar een Persoon aan een Lijst van de Marketing."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Fout aangepaste entiteit"
>abstract="Aangepaste entiteiten zijn **niet** toegestaan."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Invalid B2B entity error"
>abstract="Alleen de volgende B2B-entiteiten mogen worden gebruikt: `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member`, en `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Fout in maximumwaarden"
>abstract="Het maximumaantal waarden dat voor één veld kan worden gecontroleerd, is **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="gebeurtenisfout in inSegment"
>abstract="inSegment-gebeurtenissen zijn **niet** toegestaan."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="gebeurtenisfout in inSegment"
>abstract="inSegment-gebeurtenissen zijn **niet** toegestaan."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Opeenvolgende gebeurtenisfout"
>abstract="Sequentiële gebeurtenissen zijn **niet** toegestaan."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Eigenschappenfout toewijzen"
>abstract="Eigenschappen van het type Map zijn **niet** toegestaan."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Maximale diepte van geneste entiteit"
>abstract="De maximale diepte van geneste arrays is **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Maximale fout in aantal geneste objecten"
>abstract="Het maximale aantal toegestane geneste objecten is **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Inbreuk op beperking"
>abstract="Het publiek schendt een beperking. Lees het gekoppelde document voor meer informatie."

Bij het gebruik van accountsoorten **moet** voldoen aan de volgende beperkingen:

>[!NOTE]
>
>In de volgende lijst wordt de **default** beperkingen voor het publiek voor rekening. Deze waarden **kan** wijzigen, afhankelijk van de instellingen die door de beheerder van uw organisatie zijn geïmplementeerd.

- Het maximale terugzoekvenster voor Experience Events is **dertig dagen**.
- De maximale diepte van geneste containers is **5**.
   - Dit betekent dat u **kan** wanneer u een publiek maakt, hebt u meer dan vijf geneste containers.
- Het maximumaantal regels in één container is **5**.
   - Dit betekent dat uw publiek **kan** hebben meer dan vijf regels die uw publiek samenstellen.
- Het maximumaantal entiteiten tussen de verschillende entiteiten dat kan worden gebruikt is **5**.
   - Een kruisentiteit is wanneer u tussen verschillende entiteiten in uw publiek verandert. Bijvoorbeeld, ga van een Rekening naar een Persoon aan een Lijst van de Marketing.
- Aangepaste entiteiten **kan** worden gebruikt.
- Het maximumaantal waarden dat voor één veld kan worden gecontroleerd, is **50**.
   - Als u bijvoorbeeld een veld hebt met de naam &quot;City&quot;, kunt u die waarde controleren op 50 namen van steden.
- Accountpubliek **kan** gebruiken `inSegment` gebeurtenissen.
- Accountpubliek **kan** opeenvolgende gebeurtenissen gebruiken.
- Accountpubliek **kan** gebruiken, kaarten.
- De maximale diepte van geneste arrays is **5**.
- Het maximumaantal geneste objecten is **10**.
