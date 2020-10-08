---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Gebruikershandleiding voor beleid samenvoegen
topic: guide
translation-type: tm+mt
source-git-commit: 45f42bae4060e107e6c131659cea5d10457c34f8
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---


# Gebruikershandleiding voor beleid samenvoegen

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Deze handleiding bevat stapsgewijze instructies voor het werken met samenvoegbeleidsregels via de Adobe Experience Platform-gebruikersinterface.

Als u het samenvoegbeleid liever wilt gebruiken met de [!DNL Real-time Customer Profile] API, volgt u de instructies in de zelfstudie over de [samenvoegbeleidsAPI](../api/merge-policies.md).

## Aan de slag

Deze gids vereist een goed begrip van de verschillende [!DNL Experience Platform] diensten betrokken bij fusiebeleid. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-time klantprofiel]](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): Schakelt [!DNL Real-time Customer Profile] het overbruggen van identiteiten uit verschillende gegevensbronnen in [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

## Samenvoegbeleid weergeven

Binnen het [!DNL Experience Platform] gebruikersinterface, kunt u beginnen met het samenvoegen beleid te werken en een lijst van het bestaande de fusiebeleid van uw organisatie te zien door **[!UICONTROL Profielen]** in het linkerspoor te selecteren en dan het beleid **[!UICONTROL van de]** Fusie te selecteren tabel.

![Landingspagina van beleid samenvoegen](../images/merge-policies/landing.png)

De details voor elk samenvoegbeleid beschikbaar aan uw organisatie zijn zichtbaar op de het landen pagina, met inbegrip van de beleidsnaam, standaardsamenvoegbeleid, en schema.

Als u wilt selecteren welke details zichtbaar zijn of extra kolommen wilt toevoegen aan de weergave, selecteert u het pictogram van de kolomkiezer en klikt u op de kolomnaam om deze toe te voegen aan of te verwijderen uit de weergave.

![](../images/merge-policies/adjust-view.png)

## Samenvoegbeleid maken

Als u een nieuw samenvoegbeleid wilt maken, selecteert u **[!UICONTROL Samenvoegbeleid]** maken.

![Landingspagina van beleid samenvoegen](../images/merge-policies/create-new.png)

Het scherm **[!UICONTROL Samenvoegbeleid]** maken wordt weergegeven, zodat u belangrijke informatie voor het nieuwe samenvoegbeleid kunt opgeven.

![](../images/merge-policies/create.png)

* **[!UICONTROL Naam]**: De naam van uw samenvoegingsbeleid moet beschrijvend maar beknopt zijn.
* **[!UICONTROL Schema]**: Het schema dat is gekoppeld aan het samenvoegbeleid. Dit specificeert het schema XDM waarvoor dit fusiebeleid wordt gecreeerd. Organisaties kunnen per schema meerdere samenvoegbeleidsregels maken.
* **[!UICONTROL ID stitching]**: In dit veld wordt gedefinieerd hoe de verwante identiteiten van een klant worden bepaald. Er zijn twee mogelijke waarden:
   * **[!UICONTROL Geen]**: Geen identiteitsstitching uitvoeren.
   * **[!UICONTROL Privégrafiek]**: Identiteitsstitching uitvoeren op basis van uw persoonlijke identiteitsgrafiek.
* **[!UICONTROL Kenmerk samenvoegen]**: Een profielfragment bevat informatie voor slechts één identiteit uit de lijst met identiteiten die voor een individuele klant bestaan. Wanneer het gebruikte grafiektype van de identiteit in meer dan één identiteit resulteert, is er de mogelijkheid voor conflicterende profielattributen en de prioriteit moet worden gespecificeerd. Met &quot;[!UICONTROL Kenmerksamenvoeging]&quot; kunt u opgeven welke waarden van het gegevenssetprofiel u wilt prioriteren als er een samenvoegconflict optreedt tussen gegevenssets van het type key-value (recordgegevens). Er zijn twee mogelijke waarden:
   * **[!UICONTROL Tijdstempel geordend]**: In geval van een conflict wordt prioriteit gegeven aan het profiel dat het laatst is bijgewerkt. [!UICONTROL Tijdstempel dat is geordend] , ondersteunt ook aangepaste tijdstempels die voorrang hebben op systeemtijdstempels bij het samenvoegen van gegevens binnen dezelfde gegevensset (meerdere identiteiten) of over gegevenssets heen. Zie de [sectie met geordende](#timestamp-ordered) tijdstempels voor meer informatie.
   * **[!UICONTROL Prioriteit]** gegevensset: In geval van een conflict, geef prioriteit aan profielfragmenten die op de dataset worden gebaseerd waaruit zij kwamen. Wanneer het selecteren van deze optie, moet u de verwante datasets en hun orde van prioriteit kiezen. Zie de details over [datasetbelangrijkheid](#dataset-precedence) hieronder voor meer informatie.
* **[!UICONTROL Standaardsamenvoegbeleid]**: Een schakelknop waarmee u kunt bepalen of dit samenvoegbeleid al dan niet de standaardinstelling voor uw organisatie is. Als de kiezer wordt ingeschakeld en het nieuwe beleid wordt opgeslagen, wordt het vorige standaardbeleid automatisch bijgewerkt zodat het niet langer de standaardbeleid is.

### Tijdstempel geordend {#timestamp-ordered}

Aangezien de verslagen van het Profiel in Experience Platform worden opgenomen, wordt een systeemtimestamp verkregen op het tijdstip van opneming en toegevoegd aan het verslag. Wanneer **[!UICONTROL Tijdstempel geordend]** is geselecteerd als het samenvoegtype **[!UICONTROL voor]** kenmerken voor een samenvoegbeleid, worden profielen samengevoegd op basis van de tijdstempel van het systeem. Met andere woorden, het samenvoegen wordt uitgevoerd op basis van de tijdstempel voor het tijdstip waarop de record in het Platform is opgenomen.

Soms zijn er gebruiksgevallen waarin het nodig is een aangepaste tijdstempel op te geven en het samenvoegbeleid de aangepaste tijdstempel moet gebruiken in plaats van de systeemtijdstempel. Voorbeelden hiervan zijn het terugvullen van gegevens of het garanderen van de juiste volgorde van gebeurtenissen als records buiten de bestelling worden opgenomen.

>[!NOTE]
>
>Dit vermogen is slechts beschikbaar voor opname over datasets. Als de verslagen gebruikend de zelfde dataset worden opgenomen, komt het standaardvervangingsgedrag voor.

### Aangepaste tijdstempels gebruiken {#custom-timestamps}

Als u een aangepaste tijdstempel wilt gebruiken, moet de &quot;[!UICONTROL External Source System Audit Details Mixin]&quot; worden toegevoegd aan het profielschema. Nadat u de aangepaste tijdstempel hebt toegevoegd, kunt u deze in het `lastUpdatedDate` veld vullen.

Wanneer een verslag met het bevolkte `lastUpdatedDate` gebied wordt opgenomen, zal het Experience Platform dat gebied gebruiken om verslagen over datasets samen te voegen. Als `lastUpdatedDate` het Platform niet aanwezig of niet gevuld is, blijft het de tijdstempel van het systeem gebruiken.

>[!NOTE]
>
>U moet ervoor zorgen dat de `lastUpdatedDate` tijdstempel wordt gevuld wanneer u een update in dezelfde record opneemt.

In de volgende schermafbeelding worden de velden weergegeven in de map &quot;[!UICONTROL External Source System Audit Details Mixin]&quot;. Voor geleidelijke instructies bij het werken met schema&#39;s die UI gebruiken, met inbegrip van hoe te om mengsels aan schema&#39;s toe te voegen, gelieve te bezoeken [leerprogramma voor het creëren van een schema gebruikend UI](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

Als u met aangepaste tijdstempels wilt werken met de API, raadpleegt u de bijlage bij de eindgebruikershandleiding [voor](../api/merge-policies.md) samenvoegbeleid en de sectie over het [gebruik van aangepaste tijdstempels](../api/merge-policies.md#custom-timestamps).

### Dataset-prioriteit {#dataset-precedence}

Wanneer het selecteren van een waarde van de samenvoeging **[!UICONTROL van]** Attributen, kunt u de voorkeur **[!UICONTROL van de]** Dataset selecteren die u toestaat om prioriteit aan profielfragmenten te geven die op de dataset worden gebaseerd waaruit zij kwamen.

Een geval van het voorbeeldgebruik zou zijn als uw organisatie informatie aanwezig in één dataset had die over gegevens in een andere dataset voorkeur of vertrouwd is.

Wanneer het selecteren van de belangrijkheid **[!UICONTROL van de]** Dataset, opent een afzonderlijk paneel dat u van **[!UICONTROL Beschikbare datasets]** vereist om te selecteren welke datasets zullen worden omvat (of gebruik checkbox om allen te selecteren). U kunt die datasets dan slepen en neerzetten in het **[!UICONTROL Geselecteerde paneel van Datasets]** en hen slepen in de correcte orde van prioriteit. De hoogste dataset zal hoogste prioriteit worden gegeven, zal de tweede dataset tweede-hoogste zijn, etc.

![](../images/merge-policies/dataset-precedence.png)

Als u klaar bent met het maken van het samenvoegbeleid, selecteert u **[!UICONTROL Opslaan]** om terug te keren naar het tabblad **[!UICONTROL Samenvoegingsbeleid]** , waar het nieuwe samenvoegbeleid nu wordt weergegeven in de lijst met beleidsregels.

## Een samenvoegingsbeleid bewerken

U kunt een bestaand samenvoegbeleid wijzigen via het tabblad [!UICONTROL Samenvoegen van beleidsregels] door de **[!UICONTROL beleidsnaam]** te selecteren voor het samenvoegbeleid dat u wilt bewerken.

![Landingspagina van beleid samenvoegen](../images/merge-policies/select-edit.png)

Wanneer het **[!UICONTROL Edit scherm van het Samenvoegingsbeleid]** verschijnt, kunt u veranderingen in de naam, het schema, identiteitskaart het stitching type, en het type van attributensamenvoeging aanbrengen, evenals selecteren of dit beleid al dan niet het standaardfusiebeleid voor uw organisatie zal zijn.

>[!NOTE]
>
>U kunt de beleids-id voor samenvoegen, die boven in het bewerkingsscherm wordt weergegeven, niet bewerken. Dit is een alleen-lezen, door het systeem gegenereerde id die niet kan worden gewijzigd.

![](../images/merge-policies/edit-screen.png)

Nadat u de benodigde wijzigingen hebt aangebracht, selecteert u **[!UICONTROL Opslaan]** om terug te keren naar het tabblad **[!UICONTROL Samenvoegen van beleidsregels]** , waar de bijgewerkte informatie over het samenvoegbeleid nu wordt weergegeven.

![](../images/merge-policies/edited.png)

## Schendingen van het beleid inzake gegevensbeheer

Wanneer het creëren van of het bijwerken van een samenvoegbeleid, wordt een controle uitgevoerd om te bepalen als het fusiebeleid om het even welk beleid van het gegevensgebruik schendt dat door uw organisatie wordt bepaald. Het beleid voor gegevensgebruik maakt deel uit van Adobe Experience Platform [!DNL Data Governance] en is een regel die het soort marketingacties beschrijft dat u op specifieke [!DNL Platform] gegevens mag uitvoeren of waarvan u een beperking hebt. Bijvoorbeeld, als een fusiebeleid werd gebruikt om een segment tot stand te brengen dat aan een derdebestemming activeerde, en uw organisatie een beleid van het gegevensgebruik had dat de uitvoer van specifieke gegevens naar derden verhindert, zou u een &quot;[!UICONTROL Gegevens behoorlijk ontdekte]&quot;bericht ontvangen wanneer het proberen om uw fusiebeleid te bewaren.

Deze melding bevat een lijst met beleidsregels voor gegevensgebruik die zijn overtreden. U kunt de details van de schending bekijken door een beleid in de lijst te selecteren. Wanneer u een overtreden beleid selecteert, biedt het tabblad **[!UICONTROL Gegevenskoppeling]** de reden voor de schending en de desbetreffende activering, elk met meer details over de manier waarop het beleid voor gegevensgebruik is overtreden.

Als u meer wilt weten over de manier waarop gegevensbeheer in Adobe Experience Platform wordt uitgevoerd, leest u eerst het overzicht [van](../../data-governance/home.md)gegevensbeheer.

![](../images/merge-policies/policy-violation.png)

## Volgende stappen

Nu u samenvoegbeleid voor uw IMS-organisatie hebt gemaakt en geconfigureerd, kunt u deze gebruiken om publiekssegmenten te maken op basis van uw profielgegevens. Zie het overzicht [van de](../../segmentation/home.md) Segmentatie voor meer informatie over om tot stand te brengen en met segmenten te werken gebruikend [!DNL Experience Platform].