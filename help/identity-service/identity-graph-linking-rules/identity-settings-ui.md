---
title: Gebruikersinterface Identiteitsinstellingen
description: Leer hoe u de gebruikersinterface voor identiteitsinstellingen gebruikt.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 38d331bd9265f25a3aebdcbd20ae5fc30a93e960
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Gebruikersinterface Identiteitsinstellingen

>[!IMPORTANT]
>
>[!DNL Identity Graph Linking Rules] is nu algemeen beschikbaar. Neem contact op met uw Adobe-accountteam of de ondersteuning van Adobe als u een bestaande sandbox hebt waarvoor samengevouwen grafieken moeten worden samengevouwen (&quot;fixed&quot;) nadat u identiteitsinstellingen hebt ingeschakeld.

Identiteitsinstellingen zijn een functie in de gebruikersinterface van de Adobe Experience Platform Identity Service die u kunt gebruiken om unieke naamruimten aan te wijzen en naamruimteprioriteit te configureren.

Bekijk de volgende video voor aanvullende informatie over het gebruik van de interface [!DNL Graph Simulation] in de gebruikersinterface van de identiteitsservice:

>[!VIDEO](https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops)

Lees deze gids om te leren hoe te om uw identiteitsmontages in UI te vormen.

## Vereisten

Lees de volgende documenten voordat u begint te werken met identiteitsinstellingen:

* [[!DNL Identity Graph Linking Rules]](./overview.md)
* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Implementatiehandleiding](./implementation-guide.md)
* [Voorbeelden van grafiekconfiguraties](./example-configurations.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [Grafieksimulatie](./graph-simulation.md)

### Machtigingen instellen {#set-permissions}

Vervolgens moet u ervoor zorgen dat voor uw account de volgende machtigingen gelden:

* **[!UICONTROL View Identity Settings]**: Pas deze machtiging toe om unieke naamruimten en naamruimteprioriteit weer te geven in de pagina Bladeren naar naamruimte voor identiteit.
* **[!UICONTROL Edit Identity Settings]**: Pas deze machtiging toe om uw identiteitsinstellingen te kunnen bewerken en opslaan.

Neem contact op met de beheerder als u deze machtigingen niet hebt. Voor meer informatie, lees de [ toestemmingengids ](../../access-control/abac/ui/permissions.md).

## Uw identiteitsinstellingen configureren

Als u identiteitsinstellingen wilt openen, navigeert u naar de werkruimte Identiteitsservice in de gebruikersinterface van Adobe Experience Platform en selecteert u **[!UICONTROL Settings]** .

![ de interface van het identiteitsdashboard met de &quot;Geselecteerde knoop van Montages&quot;.](../images/rules/dashboard.png)

De pagina met identiteitsinstellingen bestaat uit twee gedeelten: [!UICONTROL Person namespaces] en [!UICONTROL Device or cookie namespaces] . Personnaamruimten zijn id&#39;s voor afzonderlijke personen. Dit kunnen apparaat-id&#39;s, e-mailadressen en telefoonnummers zijn. Apparaat- of cookie-naamruimten zijn id&#39;s voor apparaten en webbrowsers en kunnen geen hogere prioriteit krijgen dan naamruimten van personen. U kunt een apparaat- of cookie-naamruimte ook niet toewijzen als een unieke naamruimte.

### Naamruimteprioriteit configureren

Om namespace prioriteit te vormen, selecteer een namespace in het menu van identiteitsinstellingen en sleep dan en laat vallen die namespace aan de orde van uw houden. Plaats een naamruimte hoger in de lijst om deze een hogere prioriteit te geven en plaats een naamruimte lager in de lijst om deze een lagere prioriteit te geven. De naamruimte met de hoogste prioriteit moet ook als een unieke naamruimte worden opgegeven.

![ de werkruimte van identiteitsmontages met een benadrukte persoon namespace.](../images/rules/namespace-priority.png)

### Geef uw unieke naamruimte op

Als u een unieke naamruimte wilt toewijzen, schakelt u het selectievakje [!UICONTROL Unique per graph] in dat overeenkomt met die naamruimte. U kunt **tot een maximum van drie unieke namespaces** voor uw configuratie van identiteitsmontages selecteren.

Wanneer uw unieke naamruimten zijn ingesteld, kunnen grafieken niet langer meerdere identiteiten hebben die een unieke naamruimte bevatten. Als u bijvoorbeeld CRMID hebt aangewezen als een unieke naamruimte, kan een grafiek slechts één identiteit hebben met de naamruimte CRMID. Voor meer informatie, lees het [ overzicht van het Algoritme van de Optimalisering van de Identiteit ](./identity-optimization-algorithm.md#unique-namespace).

Wanneer u klaar bent met uw configuraties, selecteert u **[!UICONTROL Next]** om door te gaan.

![ twee die namespaces worden geselecteerd en als uniek worden bepaald.](../images/rules/unique-namespace.png)

Van hier, moet u het volgende bevestigen alvorens tot de definitieve stap te werk te gaan:

1. De geselecteerde unieke naamruimten.
2. Het bestaan van een identiteit met de hoogst geprioriteerde unieke naamruimte in elk bekend profiel.
3. De volgorde van de naamruimtenprioriteit.

![ A bevestigingsvenster met de &quot;bevestig&quot;geselecteerde knoop.](../images/rules/confirmation.png)

### Bevestig uw instellingen {#confirm-your-settings}

>[!IMPORTANT]
>
>* De definitieve stap is een ander bevestigingsbericht erop wijst dat de bestaande grafieken slechts door het grafiekalgoritme **zullen worden beïnvloed slechts als de grafieken na het opslaan van uw montages** worden bijgewerkt, en dat de primaire identiteit van gebeurtenisfragmenten op het Profiel van de Klant in real time niet zal worden bijgewerkt zelfs na namespace prioritaire veranderingen.
>
>* Het zal tot **24 uren** voor uw nieuwe of bijgewerkte montages duren om van kracht te worden. Voer de naam van de sandbox in en selecteer **[!UICONTROL Confirm]** om deze te bevestigen.
>
>* Uw gegevens worden pas gewijzigd wanneer u uw identiteitsinstellingen opslaat.

![ het bevestigingsvenster dat een waarschuwing over een vertraging van zes uur toont alvorens de configuraties worden verwerkt.](../images/rules/complete.png)

## Volgende stappen

Lees de volgende documentatie voor meer informatie over [!DNL Identity Graph Linking Rules] :

* [[!DNL Identity Graph Linking Rules]-overzicht](./overview.md)
* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Implementatiehandleiding](./implementation-guide.md)
* [Voorbeelden van grafiekconfiguraties](./example-configurations.md)
* [Problemen oplossen en veelgestelde vragen](./troubleshooting.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [UI voor grafieksimulatie](./graph-simulation.md)