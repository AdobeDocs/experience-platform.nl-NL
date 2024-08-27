---
title: Gebruikersinterface Identiteitsinstellingen
description: Leer hoe u de gebruikersinterface voor identiteitsinstellingen gebruikt.
badge: Beta
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 04b04807196bb5902e398403612429eae0de3988
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Gebruikersinterface voor identiteitsinstellingen

>[!AVAILABILITY]
>
>De regels voor identiteitsgrafiekkoppelingen staan momenteel in bèta. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria. De functie en documentatie kunnen worden gewijzigd.

Identiteitsinstellingen zijn een functie in de gebruikersinterface van de Adobe Experience Platform Identity Service die u kunt gebruiken om unieke naamruimten aan te wijzen en naamruimteprioriteit te configureren.

Lees deze gids om te leren hoe te om uw identiteitsmontages in UI te vormen.

## Vereisten

Lees de volgende documenten voordat u begint te werken met identiteitsinstellingen:

* [Configuratie-hulplijn voor identiteitsgrafiek met koppelingsregels](./configuration.md)
* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [Grafieksimulatie](./graph-simulation.md)

## Uw identiteitsinstellingen configureren

Als u identiteitsinstellingen wilt openen, navigeert u naar de werkruimte Identiteitsservice in de gebruikersinterface van Adobe Experience Platform en selecteert u **[!UICONTROL Settings]** .

![ de knoop van identiteitsmontages selecteerde.](../images/rules/identities-ui.png)

De pagina met identiteitsinstellingen bestaat uit twee gedeelten: [!UICONTROL Person namespaces] en [!UICONTROL Device or cookie namespaces] . Personnaamruimten zijn id&#39;s voor afzonderlijke personen. Dit kunnen apparaat-id&#39;s, e-mailadressen en telefoonnummers zijn. Apparaat- of cookie-naamruimten zijn id&#39;s voor apparaten en webbrowsers en kunnen geen hogere prioriteit krijgen dan naamruimten van personen. U kunt een apparaat- of cookie-naamruimte ook niet toewijzen als een unieke naamruimte.

### Naamruimteprioriteit configureren

Om namespace prioriteit te vormen, selecteer een namespace in het menu van identiteitsinstellingen en sleep dan en laat vallen die namespace aan de orde van uw houden. Plaats een naamruimte hoger in de lijst om deze een hogere prioriteit te geven en plaats een naamruimte lager in de lijst om deze een lagere prioriteit te geven. De naamruimte met de hoogste prioriteit moet ook als een unieke naamruimte worden opgegeven.

![ de werkruimte van identiteitsmontages met een benadrukte persoon namespace.](../images/rules/namespace-priority.png)

### Geef uw unieke naamruimte op

Als u een unieke naamruimte wilt toewijzen, schakelt u het selectievakje [!UICONTROL Unique per graph] in dat overeenkomt met die naamruimte. U kunt meer dan één unieke naamruimte selecteren voor de configuratie van uw identiteitsinstellingen.

![ twee die namespaces worden geselecteerd en als uniek worden bepaald.](../images/rules/unique-namespace.png)

Wanneer uw unieke naamruimten zijn ingesteld, kunnen grafieken niet langer meerdere identiteiten hebben die een unieke naamruimte bevatten. Als u bijvoorbeeld CRMID hebt aangewezen als een unieke naamruimte, kan een grafiek slechts één identiteit hebben met de naamruimte CRMID. Voor meer informatie, lees het [ overzicht van het algoritme van de identiteitsoptimalisering ](./identity-optimization-algorithm.md#unique-namespace).

Wanneer u klaar bent met uw configuraties, selecteert u **[!UICONTROL Next]** . Er wordt een bevestigingsbericht weergegeven. Gebruik deze gelegenheid om te controleren of uw configuraties correct zijn en selecteer vervolgens **[!UICONTROL Finish]** .

![ de bevestigingspagina met benadrukte Einde.](../images/rules/finish.png)

Een waarschuwingsbericht verschijnt, erop wijzend dat de bestaande grafieken slechts door het grafiekalgoritme zullen worden beïnvloed slechts als de grafieken **na het opslaan van uw montages** worden bijgewerkt, en dat de primaire identiteit van gebeurtenisfragmenten op het Profiel van de Klant in real time niet zal worden bijgewerkt zelfs na namespace prioritaire veranderingen. Bovendien, wordt u meegedeeld dat het tot **zes uren** voor uw nieuwe montages zal duren om van kracht te worden. Voer de naam van de sandbox in en selecteer vervolgens **[!UICONTROL Confirm]** om dit te bevestigen.

![ het bevestigingsvenster dat een waarschuwing over een vertraging van zes uur toont alvorens de configuraties worden verwerkt.](../images/rules/confirm-settings.png)

## Volgende stappen

U hebt nu de naamruimteprioriteiten geconfigureerd en uw unieke naamruimten toegewezen met behulp van de gebruikersinterface voor identiteitsinstellingen. Voor meer informatie, lees de [ identiteitsgrafiek die regels verbindt overzicht ](./overview.md).
