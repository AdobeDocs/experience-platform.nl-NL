---
keywords: Experience Platform;home;populaire onderwerpen;identiteitsgrafiekviewer;Identiteitsgrafiekviewer;grafiekviewer;Grafiekviewer;Naamruimte;Identiteitsnaamruimte;Identiteitsservice;Identiteitsservice
solution: Experience Platform
title: Overzicht van de Identity Graph Viewer
description: Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# Overzicht van de identiteitsgrafiekviewer

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat. Alle grafieken van de klantenidentiteit worden collectief beheerd en door de Dienst van de Identiteit van Adobe Experience Platform in bijna real time bijgewerkt, in antwoord op klantenactiviteit.

Met de identiteitsgrafiekviewer in de gebruikersinterface van het Platform kunt u visualiseren en beter begrijpen welke klantidentiteiten aan elkaar zijn gekoppeld en op welke manieren. Met de viewer kunt u naar verschillende delen van de grafiek slepen en hiermee communiceren, zodat u complexe identiteitsrelaties kunt onderzoeken, efficiënter kunt werken en kunt profiteren van meer transparantie bij het gebruik van informatie.

## Video over zelfstudie

De volgende video is bedoeld als ondersteuning voor uw begrip van de viewer voor identiteitsgrafieken.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Aan de slag

Als u met de viewer voor identiteitsgrafieken werkt, moet u de verschillende betrokken Adobe Experience Platform-services begrijpen. Voordat u begint te werken met de identiteitsgrafiekviewer, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Identity Service]](../home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.

### Terminologie

- **Identiteit (knooppunt):** Een identiteit of een knoop is gegevens uniek aan een entiteit, typisch een persoon. Een identiteit bestaat uit een naamruimte en identiteitswaarde.
- **Koppeling (rand):** Een koppeling of rand vertegenwoordigt de verbinding tussen identiteiten.
- **Grafiek (cluster):** Een grafiek of een cluster is een groep identiteiten en koppelingen die een persoon vertegenwoordigen.

## De viewer voor identiteitsgrafieken openen

Selecteer **[!UICONTROL Identities]** in de linkernavigatie en selecteer vervolgens de **[!UICONTROL Identity graph]** tab. Van de **[!UICONTROL Identity Namespace]** scherm, klik **[!UICONTROL Select identity namespace]** gebruiken om te zoeken naar de naamruimte die u wilt gebruiken.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

De **[!UICONTROL Select identity namespace]** wordt weergegeven. Dit scherm bevat een lijst met naamruimten die beschikbaar zijn voor uw organisatie, inclusief informatie over naamruimten **[!UICONTROL Display name]**, **[!UICONTROL Identity symbol]**, **[!UICONTROL Owner]**, **[!UICONTROL Last updated]** datum, en **[!UICONTROL Description]**. U kunt alle opgegeven naamruimten gebruiken zolang er een geldige identiteitswaarde aan is gekoppeld.

Selecteer de naamruimte die u wilt gebruiken en klik op **[!UICONTROL Select]** om verder te gaan.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Nadat u een naamruimte hebt geselecteerd, voert u de bijbehorende waarde voor een bepaalde klant in het dialoogvenster **[!UICONTROL Identity value]** tekstvak en selecteer **[!UICONTROL View]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### Toegang tot de kijker van de identiteitsgrafiek van datasets

U kunt tot de kijker van de identiteitsgrafiek ook toegang hebben gebruikend de datasetinterface. Uit de datasets [!UICONTROL Browse] pagina, selecteer een dataset u met wilt in wisselwerking staan, en dan selecteren **[!UICONTROL Preview dataset]**

![preview-dataset](../images/identity-graph-viewer/preview-dataset.png)

Selecteer in het voorvertoningsvenster een vingerafdrukpictogram om de identiteiten weer te geven die door de viewer voor identiteitsgrafieken worden weergegeven.

>[!TIP]
>
>Het vingerafdrukpictogram wordt alleen weergegeven als de gegevensset twee of meer identiteiten heeft.

![vingerafdruk](../images/identity-graph-viewer/fingerprint.png)

De viewer voor identiteitsgrafieken wordt weergegeven. Links in het scherm ziet u de identiteitsgrafiek waarin alle identiteiten worden weergegeven die zijn gekoppeld aan de naamruimte die u hebt geselecteerd en de identiteitswaarde die u hebt ingevoerd. Elk identiteitsknooppunt bestaat uit een naamruimte en de bijbehorende ID-waarde. U kunt elke gewenste identiteit selecteren en vasthouden om te slepen en met de grafiek te communiceren. U kunt de muisaanwijzer ook boven een identiteit plaatsen om informatie over de bijbehorende id-waarde weer te geven. De grafiekuitvoer wordt ook weergegeven als een ingediende lijst in het midden van het scherm.

>[!IMPORTANT]
>
>Een identiteitsgrafiek vereist een minimum van twee verbonden identiteiten om, evenals een geldige namespace en paar van identiteitskaart te produceren. Het maximumaantal identiteiten dat de grafiekviewer kan weergeven, is 150. Zie de [aanhangsel](#appendix) zie hieronder voor meer informatie .

![identiteitsgrafiek](../images/identity-graph-viewer/graph-viewer.png)

Selecteer een identiteit om de gemarkeerde rij in de **[!UICONTROL Identities]** tabel en actualisering van de informatie op het rechterspoor, met inbegrip van de **[!UICONTROL Value]**, **[!UICONTROL Batch ID]** en de **[!UICONTROL Last updated]** datum.

![select-identity](../images/identity-graph-viewer/select-identity.png)

U kunt door een grafiek filtreren en een specifieke namespace isoleren gebruikend de soortoptie bovenop **[!UICONTROL Identities]** tabel. Selecteer in het vervolgkeuzemenu de naamruimte die u wilt markeren.

![filter-voor-naamruimte](../images/identity-graph-viewer/filter-namespace.png)

De grafiekviewer retourneert een markering voor de door u geselecteerde naamruimte. De filteroptie werkt ook de **[!UICONTROL Identities]** tabel om alleen informatie te retourneren voor de naamruimte die u hebt geselecteerd.

![gefilterd](../images/identity-graph-viewer/filtered.png)

De rechterbovenhoek van het vak van de grafiekviewer bevat opties voor vergroting. Selecteer **(+)** pictogram om in de grafiek of **(-)** pictogram om uit te zoomen.

![zoomen](../images/identity-graph-viewer/zoom.png)

U kunt meer informatie over batches weergeven door de optie **[!UICONTROL Data source]** in de koptekst. De **[!UICONTROL Data source]** tabel bevat een lijst met **[!UICONTROL Batch IDs]** en **[!UICONTROL Linked IDs]**, bronschema en datum van opname.

![gegevensbron](../images/identity-graph-viewer/data-source-table.png)

U kunt om het even welke verbindingen binnen een identiteitsgrafiek selecteren om alle bronpartijen te zien die aan de verbinding hebben bijgedragen.

![select-links](../images/identity-graph-viewer/select-edge.png)

U kunt ook één batch selecteren om alle koppelingen weer te geven waarnaar deze batch heeft bijgedragen.

![select-links](../images/identity-graph-viewer/select-batch.png)

Identiteitsgrafieken met grotere clusters van identiteiten zijn ook toegankelijk via de viewer voor identiteitsgrafieken.

![groot cluster](../images/identity-graph-viewer/large-cluster.png)

## Aanhangsel

In de volgende sectie vindt u aanvullende informatie over het werken met de viewer voor identiteitsgrafieken.

### Foutberichten begrijpen

Er kunnen fouten optreden wanneer u de viewer voor identiteitsgrafieken opent. Hieronder volgt een lijst met voorwaarden en beperkingen waarmee u rekening kunt houden wanneer u werkt met de viewer voor identiteitsgrafieken.

- De geselecteerde naamruimte moet een identiteitswaarde bevatten.
- Voor het genereren van de identiteitsgrafiekviewer zijn minimaal twee gekoppelde identiteiten vereist. Het is mogelijk dat er slechts één identiteitswaarde en geen verbonden identiteiten zijn, en in dit geval zou de waarde slechts bestaan in [!DNL Profile] viewer.
- De viewer voor identiteitsgrafieken kan het maximumaantal van 150 identiteiten niet overschrijden.

![foutscherm](../images/identity-graph-viewer/error-screen.png)

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u de identiteitsgrafieken van uw klanten kunt verkennen in de gebruikersinterface van het Platform. Raadpleeg voor meer informatie over de identiteiten in Platform de [Overzicht van identiteitsservice](../home.md)

## Changelog

| Datum | Actie |
| ---- | ------ |
| 2021-01 | <ul><li>Toegevoegde ondersteuning voor het streamen van ingesloten gegevens en niet-productiesandbox.</li><li>Kleine correcties.</li></ul> |
| 2021-02 | <ul><li>De de grafiekkijker van de identiteit wordt toegankelijk gemaakt door datasetvoorproef.</li><li>Kleine correcties.</li><li>De viewer voor identiteitsgrafieken is algemeen beschikbaar.</li></ul> |
