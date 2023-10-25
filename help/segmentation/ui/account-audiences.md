---
title: Accountsoorten
description: Leer hoe u accountpubliek kunt maken en gebruiken om accountprofielen in downstreamdoelen te gebruiken.
badgeLimitedAvailability: label="Beperkte beschikbaarheid" type="Caution"
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html"
source-git-commit: ecc60ec2e7bf2ea02bd721eac1b101b0dc412ba0
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Accountpubliek

>[!IMPORTANT]
>
>Houd er rekening mee dat accountpubliek alleen beschikbaar is in de [B2B Edition van Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). Bovendien is de functionaliteit voor het accountpubliek momenteel in **beperkte beschikbaarheid**.

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

De [!UICONTROL Activate destination] wordt weergegeven. Voor meer informatie over het activeringsproces, waaronder informatie over veldtoewijzingen, leest u de [activeringsoverzicht](../../destinations/ui/activation-overview.md).

## Volgende stappen {#next-steps}

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u uw accountpubliek kunt maken en gebruiken in Adobe Experience Platform. Als u wilt weten hoe u andere soorten publiek in Platform kunt gebruiken, leest u de [Handleiding voor segmentatieservice](./overview.md).
