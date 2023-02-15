---
title: Identity Graph Viewer
description: Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 4bf939011e6246a553f67805ff99a70610782ea6
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# Identiteitsgrafiekviewer

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat. Alle grafieken van de klantenidentiteit worden collectief beheerd en door de Dienst van de Identiteit van Adobe Experience Platform in bijna real time bijgewerkt, in antwoord op klantenactiviteit.

Met de identiteitsgrafiekviewer in de gebruikersinterface van het Platform kunt u visualiseren en beter begrijpen welke klantidentiteiten aan elkaar zijn gekoppeld en op welke manieren. Met de viewer kunt u naar verschillende delen van de grafiek slepen en hiermee communiceren, zodat u complexe identiteitsrelaties kunt onderzoeken, efficiënter kunt werken en kunt profiteren van meer transparantie bij het gebruik van informatie.

Het volgende document bevat stappen voor het openen en gebruiken van de viewer voor identiteitsgrafieken in de gebruikersinterface van het Platform.

## Video over zelfstudie

De volgende video is bedoeld als ondersteuning voor uw begrip van de viewer voor identiteitsgrafieken.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Aan de slag

Als u met de viewer voor identiteitsgrafieken werkt, moet u de verschillende betrokken Adobe Experience Platform-services begrijpen. Voordat u begint te werken met de identiteitsgrafiekviewer, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Identity Service]](../home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
- [Klantprofiel in realtime](../../profile/home.md): Identiteitsgrafieken worden gebruikt door Real-Time Klantprofiel om een uitvoerige en unieke mening van uw klantenattributen en gedrag tot stand te brengen.

### Terminologie

- **Identiteit (knooppunt):** Een identiteit of een knoop is gegevens uniek aan een entiteit, typisch een persoon. Een identiteit bestaat uit een naamruimte voor identiteiten en een identiteitswaarde. Een volledig gekwalificeerde identiteit kan bijvoorbeeld bestaan uit een naamruimte voor identiteiten **E-mail**, gecombineerd met een identiteitswaarde van **robijn<span>@email.com**.
- **Koppeling (rand):** Een koppeling of rand vertegenwoordigt de verbinding tussen identiteiten. Identiteitskoppelingen bevatten eigenschappen zoals voor het eerst ingestelde en laatst bijgewerkte tijdstempels. De eerste vastgestelde tijdstempel definieert de datum en het tijdstip waarop een nieuwe identiteit aan een bestaande identiteit is gekoppeld. De laatste bijgewerkte tijdstempel definieert de datum en tijd waarop een bestaande identiteitskoppeling voor het laatst is bijgewerkt.
- **Grafiek (cluster):** Een grafiek of een cluster is een groep identiteiten en koppelingen die een persoon vertegenwoordigen.

## De viewer voor identiteitsgrafieken openen {#access-identity-graph-viewer}

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Identities]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Identity Graph]** in de lijst met tabbladen in de koptekst.

![De werkruimte Identiteiten in de interface van het Experience Platform, met het geselecteerde lusje van de Grafiek van de Identiteit.](../images/graph-viewer/identity-graph.png)

Als u een identiteitsgrafiek wilt weergeven, geeft u een naamruimte en de bijbehorende waarde op en selecteert u **[!UICONTROL View]**.

>[!TIP]
>
>Het tabelpictogram selecteren ![tabelpictogram](../images/identity-graph-viewer/table-icon.png) om een deelvenster weer te geven met een lijst van alle naamruimten die in uw organisatie beschikbaar zijn. U kunt alle naamruimten gebruiken zolang er een geldige identiteitswaarde aan is gekoppeld. Lees voor meer informatie de [Naamruimtehulplijn voor identiteit](../namespaces.md).

![An identity namespace and its corresponding value, provided in the Identity Graph lookup screen.](../images/graph-viewer/namespace-and-value.png)

## De interface van de identiteitsgrafiekviewer

De interface van de identiteitsgrafiekviewer bestaat uit verschillende elementen die u kunt gebruiken om te communiceren met en uw identiteitsgegevens beter te begrijpen.

![De interface van de identiteitsgrafiekviewer.](../images/graph-viewer/identity-graph-viewer-main.png)

In de identiteitsgrafiek worden alle identiteiten weergegeven die zijn gekoppeld aan de naamruimte en de waardecombinatie die u hebt ingevoerd. Elk knooppunt bestaat uit een naamruimte van een identiteit en de bijbehorende waarde. U kunt elk knooppunt selecteren, vasthouden en slepen om te communiceren met de grafiek. Alternatief, kunt u over een knoop bewegen om informatie over zijn overeenkomstige identiteitswaarde te zien. Selecteren **[!UICONTROL View graph]** om de grafiek te verbergen of weer te geven.

>[!IMPORTANT]
>
>Voor een identiteitsgrafiek moeten minimaal twee gekoppelde identiteiten worden gegenereerd en moet een geldige naamruimte en waardecombinatie worden gegenereerd. Het maximumaantal identiteiten dat de grafiekviewer kan weergeven, is 150. Zie de [aanhangsel](#appendix) zie hieronder voor meer informatie .

![De identiteitsgrafiekviewer met vijf gekoppelde identiteiten.](../images/graph-viewer/graph.png)

Selecteer een koppeling in de grafiek om de gegevensset en batch-id weer te geven die bijdragen aan die koppeling. Als u een koppeling selecteert, wordt ook het rechterspoor bijgewerkt en krijgt u meer informatie over de gegevensbrondetails en over eigenschappen zoals de eerste vastgestelde en laatst bijgewerkte tijdstempels.

![De identiteitsverbinding tussen de geselecteerde e-mail en GAID knopen.](../images/graph-viewer/identity-link.png)

De [!UICONTROL Identities] tabel bevat een andere weergave van uw identiteitsgegevens. In deze tabel worden de naamruimte en de combinatie van identiteitswaarden in een tabelindeling weergegeven. Als u een knooppunt in de grafiek selecteert, wordt het gemarkeerde regelitem in het dialoogvenster [!UICONTROL Identities] tabel.

![De tabel Identiteiten met de lijst met identiteiten die zijn gekoppeld in de grafiek.](../images/graph-viewer/identities-table.png)

Gebruik het vervolgkeuzemenu om de grafiekgegevens te sorteren en informatie over een specifieke naamruimte te markeren. Selecteer bijvoorbeeld **[!UICONTROL Email]** in het menu om gegevens weer te geven die specifiek zijn voor de naamruimte van de e-mailidentiteit.

![De tabel Identiteiten wordt alleen gesorteerd om e-mailgegevens weer te geven.](../images/graph-viewer/sort-email.png)

In de rechtertrack wordt informatie over een geselecteerde identiteit weergegeven, inclusief de laatste bijgewerkte tijdstempel. De juiste spoorstaaf toont ook informatie over de gegevensbron die met de geselecteerde identiteit, met inbegrip van zijn partij ID, datasetnaam, dataset identiteitskaart, en schemanaam beantwoordt.

De volgende tabel bevat aanvullende informatie over de eigenschappen van de gegevensbron die in de rechterspoorstaaf worden weergegeven:

| Gegevensbron | Beschrijving |
| --- | --- | 
| Batch-id | De automatisch gegenereerde id die overeenkomt met uw batchgegevens. |
| Dataset-id | De automatisch gegenereerde id die overeenkomt met uw gegevensset. |
| Naam gegevensset | De naam van de dataset die uw partijgegevens bevat. |
| Schemanaam | De naam van het schema. Het schema biedt een set regels die de structuur en indeling van gegevens vertegenwoordigen en valideren. |

![De rechterspoorlijn, die identiteitsgegevens, evenals informatiegegevensbron toont.](../images/graph-viewer/right-rail.png)

U kunt ook de opdracht *[!UICONTROL Data source]* voor een lijst met gegevensbronnen die een bijdrage leveren aan uw identiteiten. Selecteren [!UICONTROL Data source] voor een tabelweergave van uw gegevenssets en batch-id&#39;s.

![Het tabblad Gegevensbron is geselecteerd.](../images/graph-viewer/data-source-table.png)

Gebruik de schuifregelaar om grafiekgegevens te filteren op het tijdstip waarop de identiteiten voor het eerst zijn vastgesteld. Standaard worden in de viewer voor identiteitsgrafieken alle identiteiten weergegeven die in de grafiek zijn gekoppeld. Houd de schuifregelaar ingedrukt en sleep deze om de tijd aan te passen aan de laatste tijdstempel waarbij een nieuwe identiteit aan de grafiek is gekoppeld. In het onderstaande voorbeeld ziet u dat de meest recente identiteitslink (GAID) is ingesteld op **[!UICONTROL 08/19/2020, 4:29:29 PM]**.

![De schuifregelaar voor tijdstempels van de grafiekviewer is geselecteerd.](../images/graph-viewer/slider-one.png)

Pas de schuifregelaar aan om te zien of er een andere identiteitskoppeling (e-mail) is gemaakt op **[!UICONTROL 08/19/2020, 4:25:30 PM]**.

![De tijdstempelschuifregelaar van de grafiekviewer is aangepast aan de laatst ingestelde nieuwe koppeling.](../images/graph-viewer/slider-two.png)

U kunt de schuifregelaar ook aanpassen om de oudste herhaling van de grafiek te zien. In het onderstaande voorbeeld wordt in de viewer voor identiteitsgrafieken weergegeven dat de grafiek voor het eerst is gemaakt op **[!UICONTROL 08/19/2020, 4:11:49 PM]**, waarbij de eerste koppelingen ECID, Email en Phone zijn.

![De tijdstempelschuifregelaar van de grafiekviewer is aangepast aan de eerste nieuwe koppeling.](../images/graph-viewer/slider-three.png)

## Aanhangsel

In de volgende sectie vindt u aanvullende informatie over het werken met de viewer voor identiteitsgrafieken.

### Foutberichten begrijpen

Er kunnen fouten optreden wanneer u de viewer voor identiteitsgrafieken opent. Hieronder volgt een lijst met voorwaarden en beperkingen waarmee u rekening kunt houden wanneer u werkt met de viewer voor identiteitsgrafieken.

- De geselecteerde naamruimte moet een identiteitswaarde bevatten.
- Voor het genereren van de identiteitsgrafiekviewer zijn minimaal twee gekoppelde identiteiten vereist. Het is mogelijk dat er slechts één identiteitswaarde en geen verbonden identiteiten zijn, en in dit geval zou de waarde slechts bestaan in [!DNL Profile] viewer.
- De viewer voor identiteitsgrafieken kan het maximumaantal van 150 identiteiten niet overschrijden.

![foutscherm](../images/graph-viewer/error-screen.png)

### Toegang tot de kijker van de identiteitsgrafiek van datasets

U kunt tot de kijker van de identiteitsgrafiek ook toegang hebben gebruikend de datasetinterface. Uit de datasets [!UICONTROL Browse] pagina, selecteer een dataset u met wilt in wisselwerking staan, en dan selecteren **[!UICONTROL Preview dataset]**

![preview-dataset](../images/identity-graph-viewer/preview-dataset.png)

Selecteer in het voorvertoningsvenster een vingerafdrukpictogram om de identiteiten weer te geven die door de viewer voor identiteitsgrafieken worden weergegeven.

>[!TIP]
>
>Het vingerafdrukpictogram wordt alleen weergegeven als de gegevensset twee of meer identiteiten heeft.

![vingerafdruk](../images/identity-graph-viewer/fingerprint.png)

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u de identiteitsgrafieken van uw klanten kunt verkennen in de gebruikersinterface van het Platform. Raadpleeg voor meer informatie over de identiteiten in Platform de [Overzicht van identiteitsservice](../home.md)

## Changelog

| Datum | Actie |
| ---- | ------ |
| 2021-01 | <ul><li>Toegevoegde ondersteuning voor het streamen van ingesloten gegevens en niet-productiesandbox.</li><li>Kleine correcties.</li></ul> |
| 2021-02 | <ul><li>De de grafiekkijker van de identiteit wordt toegankelijk gemaakt door datasetvoorproef.</li><li>Kleine correcties.</li><li>De viewer voor identiteitsgrafieken is algemeen beschikbaar.</li></ul> |
| 2023-01 | <ul><li>UI-updates.</li></ul> |
