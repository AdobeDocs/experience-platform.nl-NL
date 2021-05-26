---
solution: Experience Platform
title: Toegang voor dashboards van Experience Platforms verkrijgen en verlenen
type: Documentation
description: Gebruikers de mogelijkheid bieden om dashboards van Experience Platforms weer te geven, te bewerken en bij te werken met Adobe Admin Console.
source-git-commit: 36aaccddeb207e22a22d5124ec8592ac8dddf8bc
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---


# Toegangsmachtigingen voor dashboards

Als u gebruikers de mogelijkheid wilt geven om dashboards weer te geven, te bewerken en bij te werken, moet u eerst machtigingen inschakelen. In Adobe Experience Platform wordt de toegangscontrole verzorgd via de Adobe Admin Console. Deze functionaliteit gebruikt productprofielen in [!DNL Admin Console], die gebruikers met toestemmingen en zandbakken verbinden.

Dit document bevat een overzicht van hoe u toegang kunt bieden tot specifieke dashboardmachtigingen in de Admin Console. Voor gedetailleerde informatie over het verkrijgen van en het toewijzen van toegangstoestemmingen, gelieve te beginnen door [toegangsbeheeroverzicht](../access-control/home.md) te lezen.

>[!NOTE]
>
>Om toegangsbeheer voor [!DNL Experience Platform] te vormen, moet u beheerdervoorrechten voor een organisatie hebben die [!DNL Experience Platform] productintegratie heeft. Zie het Adobe Help Center-artikel over [beheerrollen](https://helpx.adobe.com/enterprise/using/admin-roles.html) voor meer informatie.

## Beschikbare machtigingen {#available-permissions}

Er zijn twee belangrijke toestemmingen die worden vereist om tot dashboards binnen Experience Platform toegang te hebben. Deze machtigingen zijn:

* **Licentiegebruiksdashboard** weergeven: Met deze machtiging hebben gebruikers alleen-lezentoegang tot het dashboard voor licentiegebruik in de gebruikersinterface van het Experience Platform.
* **Standaarddashboards** beheren: Deze toestemming staat gebruikers toe om douaneattributen toe te voegen die nog niet in het gegevenspakhuis zijn.

In de volgende stappen wordt getoond hoe u deze machtigingen met Admin Console kunt toevoegen.

## Productprofielen selecteren

Als u gebruikers toegang wilt geven tot dashboards in Experience Platform, begint u met het aanmelden bij [Adobe Admin Console](https://adminconsole.adobe.com) en selecteert u **Products** in de bovenste navigatie.

![](images/admin-console/admin-console-overview.png)

Selecteer **Adobe Experience Platform** in het vervolgkeuzemenu Experience Cloud in de linkernavigatie of uit de kaarten die onder *Alle producten en services* worden vermeld. Selecteer op de Adobe Experience Platform-productpagina het productprofiel waaraan u de dashboardmachtigingen wilt toevoegen of selecteer **Nieuw profiel** om een nieuw productprofiel te maken.

![](images/admin-console/products.png)

Het geselecteerde productprofiel wordt geopend en hierin worden de gebruikers weergegeven die aan dat productprofiel zijn gekoppeld. Selecteer **Machtigingen** om de machtigingen voor het productprofiel te beheren.

![](images/admin-console/product-users.png)

## Machtigingen toevoegen/bewerken

Op het tabblad **Machtigingen** worden alle beschikbare machtigingen voor het productprofiel weergegeven. Zoek de rij **Dashboards** op en zie dat momenteel &quot;0 van 2 inbegrepen&quot;wordt vermeld, betekent dit dat er geen dashboardtoestemmingen die voor het productprofiel worden toegelaten.

Als u de dashboardmachtigingen wilt bewerken, selecteert u **Bewerken** in de dashboardrij.

![](images/admin-console/product-permissions.png)

Het dialoogvenster **Machtigingen bewerken** wordt geopend, waarin beschikbare machtigingsitems worden weergegeven en machtigingsitems zijn opgenomen. U kunt het plusteken (`+`) naast de toestemming selecteren om het toe te voegen of **+ te selecteren voeg allen** toe om alle toestemmingen meteen toe te voegen.

Voor beschrijvingen van de toestemmingen, gelieve te verwijzen naar [beschikbare toestemmingen](#available-permissions) sectie vroeger in dit document.

>[!NOTE]
>
>U hoeft niet alle machtigingen voor alle gebruikers in te schakelen. Afhankelijk van de structuur van uw organisatie kunt u verschillende productprofielen voor bepaalde gebruikers maken en beperkte toegang (zoals alleen-lezen) verlenen.

Nadat de toestemmingen zijn toegevoegd, uitgezocht **sparen** om aan het productprofiel terug te keren.

![](images/admin-console/dashboard-permissions.png)

Wanneer u naar het productprofiel terugkeert, kunt u verifiëren dat de toestemmingen zijn toegevoegd door te bevestigen dat **Dashboards** de rij &quot;2 van 2 inbegrepen&quot;toont.

![](images/admin-console/product-permissions-included.png)

## Volgende stappen

Nu u toegangstoestemmingen aan dashboards hebt toegevoegd, kunnen de gebruikers binnen uw organisatie beginnen om dashboards binnen het Experience Platform UI te bekijken en andere acties uit te voeren die op de toestemmingen worden gebaseerd die u hebt toegewezen.