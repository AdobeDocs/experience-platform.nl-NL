---
title: Identiteitsgrafiekkoppelingsregels
description: Leer over de Regels van de Vereniging van de Grafiek van Identiteit in de Dienst van de Identiteit.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 0aefcfbbbed675a08d9e3023b9f667ec59874e46
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 0%

---

# [!DNL Identity Graph Linking Rules]-overzicht {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="Koppelingsregels voor identiteitsgrafiek"
>abstract="Om deze ongewenste fusies te verhinderen, kunt u configuraties gebruiken die door de Regels van de Vereniging van de Grafiek van de Identiteit worden verstrekt en voor nauwkeurige verpersoonlijking voor uw gebruikers toestaan."

>[!IMPORTANT]
>
>Neem contact op met uw Adobe-accountteam als u een bestaande sandbox hebt waarvoor samengevouwen grafieken moeten worden verwijderd (&quot;fixed&quot;) nadat u identiteitsinstellingen hebt ingeschakeld.

Met Adobe Experience Platform Identity Service en Real-Time Customer Profile is het eenvoudig om aan te nemen dat uw gegevens perfect zijn opgenomen en dat alle samengevoegde profielen één persoon vertegenwoordigen via een personenteken, zoals een CRMID. Er zijn echter scenario&#39;s waarin bepaalde gegevens kunnen proberen meerdere verschillende profielen samen te voegen tot één profiel (grafiek samenvouwen). Om deze ongewenste samenvoegingen te voorkomen, kunt u configuraties gebruiken die via [!DNL Identity Graph Linking Rules] worden geleverd en nauwkeurige personalisatie voor uw gebruikers mogelijk maken.

## Aan de slag

De volgende documenten zijn essentieel voor het begrijpen van [!DNL Identity Graph Linking Rules] .

* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Implementatiehandleiding](./implementation-guide.md)
* [Voorbeelden van grafiekconfiguraties](./example-configurations.md)
* [Problemen oplossen en veelgestelde vragen](./troubleshooting.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [UI voor grafieksimulatie](./graph-simulation.md)
* [Gebruikersinterface voor identiteitsinstellingen](./identity-settings-ui.md)

## Videobibliotheek

Bekijk de volgende video&#39;s om meer te leren over enkele fundamentele aspecten van de regels voor identiteitsgrafiek.

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity Graph Linking Rules: Overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://video.tv.adobe.com/v/3448278/?learn=on&enablevpops&captions=dut" title="Identiteitskaart Grafiek verbindt Regels: Overzicht" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429845/?format=jpeg&nocache=1732633205780" alt="Identiteitskaart Grafiek verbindt Regels: Overzicht"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://video.tv.adobe.com/v/3448278/?learn=on&enablevpops&captions=dut" target="_blank" rel="referrer" title="Identiteitskaart Grafiek verbindt Regels: Overzicht"> Grafiek die van de Identiteit Regels verbindt: Overzicht </a>
                    </p>
                    <p class="is-size-6">Bekijk deze video voor een overzicht van de Lijnen van de Grafiek van de Identiteit en leer hoe u dit vermogen kunt gebruiken om grafiekondergang te verhinderen.</p>
                </div>
                <div style="display: flex; flex-direction; row;">
                  <a href="https://video.tv.adobe.com/v/3448278/?learn=on&enablevpops&captions=dut" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> Controle </span>
                  </a>
                  <a href="./overview.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="margin-top: 1rem; margin-left: 0.5rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> Gelezen </span>
                  </a>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity Graph Linking Rules: Identity Settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" title="Identiteitskaart Grafiek verbindt Regels: De Montages van de Identiteit" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3441086/?format=jpeg&nocache=1732633205785&captions=dut" alt="Identiteitskaart Grafiek verbindt Regels: De Montages van de Identiteit"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" target="_blank" rel="referrer" title="Identiteitskaart Grafiek verbindt Regels: De Montages van de Identiteit"> Grafiek die van de Identiteit Regels verbindt: De Montages van de Identiteit </a>
                    </p>
                    <p class="is-size-6">Bekijk deze video om te leren hoe u uw identiteitsinstellingen kunt configureren en identiteitsgrafieken van hoge kwaliteit en klantprofielen kunt maken voor Adobe Experience Platform-toepassingen zoals Real-Time CDP, Adobe Journey Optimizer en Customer Journey Analytics.</p>
                </div>
                <div style="display: flex; flex-direction: row;">
                  <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> Controle </span>
                  </a>
                  <a href="identity-settings-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="margin-top: 1rem; margin-left: 0.5rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> Gelezen </span>
                  </a>
                </div>            
            </div>
        </div>
    </div>
</div>

## Grafieksamenvouwscenario&#39;s {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="Grafiek vouwscenario&#39;s"
>abstract="Er zijn meerdere redenen waarom grafieken kunnen &#39;samenvouwen&#39; of meerdere personen-entiteiten kunnen vertegenwoordigen."

In deze sectie worden voorbeeldscenario&#39;s beschreven die u in overweging kunt nemen bij het configureren van [!DNL Identity Graph Linking Rules] .

### Gedeeld apparaat

Er zijn gevallen waarin meerdere aanmeldingen op één apparaat kunnen plaatsvinden:

| Gedeeld apparaat | Beschrijving |
| --- | --- |
| Familiecomputers en -tablets | Echtgenoot en echtgenote melden zich beide aan bij hun bankrekening. |
| Openbare kiosk | Reizigers op een luchthaven melden zich aan met hun loyaliteitsidentiteitskaart om zakken in te checken en instapkaarten af te drukken. |
| Bellen | Het personeel van het centrum van de vraag login op één enkel apparaat namens klanten die klantensteun roepen om kwesties op te lossen. |

![ een diagram van sommige gemeenschappelijke gedeelde apparaten.](../images/identity-settings/shared-devices.png)

In deze gevallen, vanuit grafiekstandpunt, zonder toegelaten grenzen, zal één enkele ECID met veelvoudige CRMIDs worden verbonden.

Met [!DNL Identity Graph Linking Rules] kunt u:

* Vorm identiteitskaart die voor login als uniek herkenningsteken wordt gebruikt. U kunt bijvoorbeeld een grafiek beperken tot het opslaan van slechts één identiteit met een CRMID-naamruimte en zo die CRMID definiëren als de unieke id van een gedeeld apparaat.
   * Op deze manier kunt u ervoor zorgen dat CRMID&#39;s niet worden samengevoegd met de ECID.

### Ongeldige scenario&#39;s voor e-mail/telefoon

Er zijn ook instanties van gebruikers die valse waarden als telefoonaantallen en/of e-mailadressen verstrekken wanneer het registreren. In deze gevallen, als de grenzen niet worden toegelaten, dan zal telefoon/e-mail verwante identiteiten uiteindelijk worden verbonden met veelvoudige verschillende CRMIDs.

![ een diagram dat ongeldige e-mail of telefoonscenario&#39;s vertegenwoordigt.](../images/identity-settings/invalid-email-phone.png)

Met [!DNL Identity Graph Linking Rules] kunt u:

* Configureer de CRMID, het telefoonnummer of het e-mailadres als de unieke id en beperkt zo één persoon tot slechts één CRMID, telefoonnummer en/of e-mailadres dat aan zijn account is gekoppeld.

### Onjuiste of onjuiste identiteitswaarden

Er zijn gevallen waarin niet-unieke, onjuiste identiteitswaarden in het systeem worden opgenomen, ongeacht de naamruimte. Voorbeelden zijn:

* IDFA-naamruimte met de identiteitswaarde &quot;user_null&quot;.
   * IDFA-identiteitswaarden moeten uit 36 tekens bestaan: 32 alfanumerieke tekens en vier afbreekstreepjes.
* Naamruimte voor telefoonnummers met de identiteitswaarde &quot;not-specified&quot;.
   * Telefoonnummers mogen geen alfabet bevatten.

Deze identiteiten zouden in de volgende grafieken kunnen resulteren, waar veelvoudige CRMIDs samen met de &quot;slechte&quot;identiteit worden samengevoegd:

![ een grafiekvoorbeeld van identiteitsgegevens met onjuiste of slechte identiteitswaarden.](../images/identity-settings/bad-data.png)

Met [!DNL Identity Graph Linking Rules] kunt u de CRMID configureren als de unieke id om te voorkomen dat ongewenst profiel samenvouwt als gevolg van dit type gegevens.

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

Met [!DNL Identity Graph Linking Rules] kunt u:

* Maak één identiteitsgrafiek/samengevoegd profiel voor elke gebruiker door unieke naamruimten te configureren, waardoor twee verschillende personen-id&#39;s niet in één identiteitsgrafiek kunnen worden samengevoegd.
* Online geverifieerde gebeurtenissen aan de persoon koppelen door prioriteiten te configureren

### Terminologie {#terminology}

| Terminologie | Beschrijving |
| --- | --- |
| Unieke naamruimte | Een unieke naamruimte is een naamruimte voor identiteiten die is ingesteld op scheiding binnen de context van een identiteitsgrafiek. U kunt een naamruimte zo configureren dat deze uniek is met behulp van de gebruikersinterface. Zodra een naamruimte als uniek is gedefinieerd, kan een grafiek slechts één identiteit hebben die die naamruimte bevat. |
| Prioriteit naamruimte | De prioriteit Namespace verwijst naar het relatieve belang van namespaces in vergelijking met elkaar. De prioriteit van Namespace is configureerbaar door UI. U kunt naamruimten in een bepaalde identiteitsgrafiek rangschikken. Zodra toegelaten, zal de namenprioriteit in diverse scenario&#39;s, zoals input voor het Algoritme van de Optimalisering van de Identiteit en bepalend primaire identiteit voor de fragmenten van de ervaringsgebeurtenis worden gebruikt. |
| Algoritme voor identiteitsoptimalisatie | Het algoritme van de Optimalisering van de Identiteit zorgt ervoor dat de richtlijnen die door een unieke namespace en namespaceprioriteiten worden gecreeerd in een bepaalde identiteitsgrafiek worden gehandhaafd. |

### Unieke naamruimte {#unique-namespace}

U kunt een naamruimte zo configureren dat deze uniek is met behulp van de gebruikersinterface voor identiteitsinstellingen. Het doen van dit, informeert het Algoritme van de Optimalisering van de Identiteit dat een bepaalde grafiek slechts één identiteit kan hebben die die unieke namespace bevat. Zo voorkomt u dat twee verschillende personen-id&#39;s in dezelfde grafiek worden samengevoegd.

Overweeg het volgende scenario:

* Scott gebruikt een tablet en opent zijn browser van Google Chrome om naar acme <span>.com te gaan, waar hij binnen ondertekent en voor nieuwe basketbalschoenen doorbladert.
   * In dit scenario worden achter de schermen de volgende identiteiten geregistreerd:
      * Een ECID-naamruimte en -waarde die het gebruik van de browser vertegenwoordigen
      * Een CRMID-naamruimte en -waarde die de geverifieerde gebruiker vertegenwoordigen (Scott is aangemeld met zijn combinatie van gebruikersnaam en wachtwoord).
* Zijn zoon Peter gebruikt dan hetzelfde tablet en gebruikt ook Google Chrome om naar acme <span>.com te gaan, waar hij zich aanmeldt voor zijn eigen rekening om naar voetbalapparatuur te zoeken.
   * In dit scenario worden achter de schermen de volgende identiteiten geregistreerd:
      * Dezelfde ECID-naamruimte en -waarde die de browser vertegenwoordigen.
      * Een nieuwe CRMID-naamruimte en -waarde die de geverifieerde gebruiker vertegenwoordigen.

Als CRMID als unieke namespace werd gevormd, dan verdeelt het algoritme van de identiteitsoptimalisering CRMIDs afzonderlijk in twee afzonderlijke identiteitsgrafieken, in plaats van hen samen te voegen.

Als u geen unieke naamruimte configureert, kan het gebeuren dat er ongewenste grafieksamenvoegingen plaatsvinden, zoals twee identiteiten met dezelfde CRMID-naamruimte, maar verschillende identiteitswaarden (scenario&#39;s zoals deze vertegenwoordigen vaak twee verschillende persoonentiteiten in dezelfde grafiek).

U moet een unieke naamruimte configureren om het algoritme voor identiteitsoptimalisatie te informeren om beperkingen op te leggen aan de identiteitsgegevens die in een bepaalde identiteitsgrafiek worden opgenomen.

### Prioriteit naamruimte {#namespace-priority}

De prioriteit Namespace verwijst naar het relatieve belang van namespaces in vergelijking met elkaar. De prioriteit Namespace is configureerbaar door UI en u kunt namespaces in een bepaalde identiteitsgrafiek rangschikken.

Één manier waarin namespace prioriteit wordt gebruikt is in het bepalen van de primaire identiteit van de fragmenten van de ervaringsgebeurtenis (gebruikersgedrag) in het Profiel van de Klant in real time. Als prioritaire montages worden gevormd, dan zal het primaire identiteitsplaatsen op Web SDK niet meer worden gebruikt om te bepalen welke profielfragmenten worden opgeslagen.

Unieke naamruimten en naamruimteprioriteiten kunnen beide worden geconfigureerd in de gebruikersinterface voor identiteitsinstellingen. De effecten van hun configuraties zijn echter anders:

| | Identiteitsservice | Realtime-klantenprofiel |
| --- | --- | --- |
| Unieke naamruimte | In de Dienst van de Identiteit, verwijst het Algoritme van de Optimalisering van de Identiteit naar unieke namespaces om de identiteitsgegevens te bepalen die aan een bepaalde identiteitsgrafiek worden opgenomen. | Unieke naamruimten zijn niet van invloed op het realtime klantprofiel. |
| Prioriteit naamruimte | In de Dienst van de Identiteit, voor grafieken die veelvoudige lagen hebben, zal namespace prioriteit bepalen dat de aangewezen verbindingen worden verwijderd. | Wanneer een ervaringsgebeurtenis in Profiel wordt opgenomen, wordt namespace met de hoogste prioriteit de primaire identiteit van het profielfragment. |

* De prioriteit Namespace heeft geen invloed op het grafiekgedrag wanneer de limiet van 50 identiteiten per grafiek wordt bereikt.
* **de prioriteit van Namespace is een numerieke waarde** die aan namespace wordt toegewezen die op zijn relatieve belang wijst. Dit is een eigenschap van een naamruimte.
* **Primaire identiteit is de identiteit waarin een profielfragment tegen** wordt opgeslagen. Een profielfragment is een record met gegevens waarin informatie over een bepaalde gebruiker wordt opgeslagen: kenmerken (gewoonlijk opgenomen via CRM-records) of gebeurtenissen (gewoonlijk opgenomen via ervaringsgebeurtenissen of online gegevens).
* De prioriteit Namespace bepaalt de primaire identiteit voor de fragmenten van de ervaringsgebeurtenis.
   * Voor profielrecords kunt u de schemawerkruimte in de Experience Platform-gebruikersinterface gebruiken om identiteitsvelden te definiëren, inclusief de primaire identiteit. Lees de gids op [ bepalend identiteitsgebieden in UI ](../../xdm/ui/fields/identity.md) voor meer informatie.
* Als een ervaringsgebeurtenis twee of meer identiteiten van de hoogste namespace prioriteit in identityMap heeft, zal het van opname worden verworpen omdat het als &quot;slechte gegevens&quot;zal worden beschouwd. Als identityMap bijvoorbeeld `{ECID: 111, CRMID: John, CRMID: Jane}` bevat, wordt de gehele gebeurtenis als ongeldige gegevens afgewezen, omdat dit betekent dat de gebeurtenis tegelijkertijd aan zowel `CRMID: John` als `CRMID: Jane` wordt gekoppeld.

Voor meer informatie, lees de gids over [ namespace prioriteit ](./namespace-priority.md).

## Volgende stappen

Lees de volgende documentatie voor meer informatie over [!DNL Identity Graph Linking Rules] :

* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Implementatiehandleiding](./implementation-guide.md)
* [Voorbeelden van grafiekconfiguraties](./example-configurations.md)
* [Problemen oplossen en veelgestelde vragen](./troubleshooting.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [UI grafieksimulatie](./graph-simulation.md)
* [Gebruikersinterface voor identiteitsinstellingen](./identity-settings-ui.md)