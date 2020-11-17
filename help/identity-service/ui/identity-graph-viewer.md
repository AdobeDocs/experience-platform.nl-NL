---
keywords: Experience Platform;home;popular topics;identity graph viewer;Identity graph viewer;graph viewer;Graph viewer;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: tutorial
description: Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat.
translation-type: tm+mt
source-git-commit: af7eab0599b17be55d5a4c129f7ebaeba91333bc
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# (bètaversie) Identiteitsgrafiekviewer

>[!NOTE]
>
>De viewer voor identiteitsgrafieken bevindt zich momenteel in bètaversie. De kenmerken van de functie kunnen worden gewijzigd.

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat. Alle grafieken van de klantenidentiteit worden collectief beheerd en door de Dienst van de Identiteit van Adobe Experience Platform in bijna real time bijgewerkt, in antwoord op klantenactiviteit.

Met de identiteitsgrafiekviewer in de gebruikersinterface van het Platform kunt u visualiseren en beter begrijpen welke klantidentiteiten aan elkaar zijn gekoppeld en op welke manieren. Met de viewer kunt u naar verschillende delen van de grafiek slepen en hiermee communiceren, zodat u complexe identiteitsrelaties kunt onderzoeken, efficiënter kunt werken en kunt profiteren van meer transparantie bij het gebruik van informatie.

## Aan de slag

Als u met de viewer voor identiteitsgrafieken werkt, moet u de verschillende betrokken Adobe Experience Platform-services begrijpen. Voordat u begint te werken met de identiteitsgrafiekviewer, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Identity Service]](../home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.

### Terminologie

- **Identiteit (knooppunt):** Een identiteit of een knoop is gegevens uniek aan een entiteit, typisch een persoon. Een identiteit bestaat uit een naamruimte en identiteitswaarde.
- **Koppeling (rand):** Een koppeling of rand vertegenwoordigt de verbinding tussen identiteiten.
- **Grafiek (cluster):** Een grafiek of een cluster is een groep identiteiten en koppelingen die een persoon vertegenwoordigen.

## De viewer voor identiteitsgrafieken openen

Als u de viewer voor identiteitsgrafieken in de gebruikersinterface wilt gebruiken, selecteert u **[!UICONTROL Identiteiten]** in de linkernavigatie en selecteert u vervolgens het tabblad **[!UICONTROL Identiteitsgrafiek]** . Klik in het scherm **[!UICONTROL Identiteitsnaamruimte]** op het pictogram Identiteitsnaamruimte **** selecteren om te zoeken naar de naamruimte die u wilt gebruiken.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

Het deelvenster Naamruimte **** selecteren wordt weergegeven. Dit scherm bevat een lijst met naamruimten die beschikbaar zijn voor uw organisatie, waaronder informatie over de **[!UICONTROL weergavenaam]** van een naamruimte, het **[!UICONTROL identiteitssymbool]**, de **[!UICONTROL eigenaar]**, de **[!UICONTROL laatst bijgewerkte]** datum en de **[!UICONTROL beschrijving]**. U kunt alle opgegeven naamruimten gebruiken zolang er een geldige identiteitswaarde aan is gekoppeld.

Selecteer de naamruimte die u wilt gebruiken en klik op **[!UICONTROL Selecteren]** om door te gaan.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Nadat u een naamruimte hebt geselecteerd, voert u de bijbehorende waarde voor een bepaalde klant in het tekstvak **[!UICONTROL Identiteitswaarde]** in en selecteert u **[!UICONTROL Weergave]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

De viewer voor identiteitsgrafieken wordt weergegeven. Links in het scherm ziet u de identiteitsgrafiek waarin alle identiteiten worden weergegeven die zijn gekoppeld aan de naamruimte die u hebt geselecteerd en de identiteitswaarde die u hebt ingevoerd. Elk identiteitsknooppunt bestaat uit een naamruimte en de bijbehorende ID-waarde. U kunt elke gewenste identiteit selecteren en vasthouden om te slepen en met de grafiek te communiceren. U kunt de muisaanwijzer ook boven een identiteit plaatsen om informatie over de bijbehorende id-waarde weer te geven. De grafiekuitvoer wordt ook weergegeven als een ingediende lijst in het midden van het scherm.

>[!IMPORTANT]
>
>Een identiteitsgrafiek vereist een minimum van twee verbonden identiteiten om, evenals een geldige namespace en paar van identiteitskaart te produceren. Het maximumaantal identiteiten dat de grafiekviewer kan weergeven, is 400. Zie de [bijlage](#appendix) hieronder voor meer informatie.

![identiteitsgrafiek](../images/identity-graph-viewer/graph-viewer.png)

Selecteer een identiteit om de gemarkeerde rij in de tabel **[!UICONTROL Identiteiten]** bij te werken en de gegevens op de rechtertrack bij te werken, waaronder de **[!UICONTROL waarde]** van een identiteit, de **[!UICONTROL Batch-id]** en de **[!UICONTROL laatst bijgewerkte]** datum.

![select-identity](../images/identity-graph-viewer/select-identity.png)

U kunt door een grafiek filtreren en een specifieke namespace isoleren gebruikend de soortoptie bovenop de lijst van **[!UICONTROL Identiteiten]** . Selecteer in het vervolgkeuzemenu de naamruimte die u wilt markeren.

![filter-voor-naamruimte](../images/identity-graph-viewer/filter-namespace.png)

De grafiekviewer retourneert een markering voor de door u geselecteerde naamruimte. De filteroptie werkt ook de tabel **[!UICONTROL Identiteiten]** bij om alleen informatie te retourneren voor de naamruimte die u hebt geselecteerd.

![gefilterd](../images/identity-graph-viewer/filtered.png)

De rechterbovenhoek van het vak van de grafiekviewer bevat opties voor vergroting. Selecteer het pictogram **(+)** om in te zoomen op de grafiek of het pictogram **(-)** om uit te zoomen.

![zoomen](../images/identity-graph-viewer/zoom.png)

U kunt meer informatie over batches weergeven door de **[!UICONTROL gegevensbron]** in de koptekst te selecteren. De **[!UICONTROL gegevensbronlijst]** toont een lijst van **[!UICONTROL Partij IDs]** verbonden aan grafiek, evenals zijn **[!UICONTROL Gekoppelde IDs]**, bronschema, en datum van opname.

![gegevensbron](../images/identity-graph-viewer/data-source-table.png)

U kunt om het even welke verbindingen binnen een identiteitsgrafiek selecteren om alle bronpartijen te zien die aan de verbinding hebben bijgedragen.

![select-links](../images/identity-graph-viewer/select-edge.png)

U kunt ook één batch selecteren om alle koppelingen weer te geven waarnaar deze batch heeft bijgedragen.

![select-links](../images/identity-graph-viewer/select-batch.png)

Identiteitsgrafieken met grotere clusters van identiteiten zijn ook toegankelijk via de viewer voor identiteitsgrafieken.

![groot cluster](../images/identity-graph-viewer/large-cluster.png)

## Aanhangsel

De grafiekviewer retourneert een fout als niet aan de volgende voorwaarden wordt voldaan:

- De identiteitswaarde bestaat niet in de geselecteerde naamruimte.
- De grafiek heeft minder dan twee identiteiten.
- De grafiek overschrijdt het maximum van 400 identiteiten.

![groot cluster](../images/identity-graph-viewer/error-screen.png)

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u de identiteitsgrafieken van uw klanten kunt verkennen in de gebruikersinterface van het Platform. Voor meer informatie over identiteiten in Platform, gelieve te verwijzen naar het overzicht van de Dienst van de [Identiteit](../home.md)