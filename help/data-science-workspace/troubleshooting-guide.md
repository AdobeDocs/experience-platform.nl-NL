---
keywords: Experience Platform;problemen oplossen;Data Science Workspace;populaire onderwerpen
solution: Experience Platform
title: Handleiding voor probleemoplossing in de Data Science Workspace
topic-legacy: Troubleshooting
description: In dit document worden antwoorden gegeven op veelgestelde vragen over de Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: ec42d80e695ccf57c10c539ae1b5104c7948c473
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# [!DNL Data Science Workspace] gids voor problemen

Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Data Science Workspace]. Voor vragen en problemen met betrekking tot [!DNL Platform] API&#39;s in het algemeen, raadpleegt u de [Handleiding voor problemen met de Adobe Experience Platform API](../landing/troubleshooting.md).

## JupyterLab-laptopquerystatus zit vast in uitvoeringsstatus

Een JupyterLab-laptop geeft mogelijk aan dat een cel zich in de uitvoeringsstatus bevindt, voor onbepaalde tijd, in sommige gevallen onder onvoldoende geheugen. Bijvoorbeeld, wanneer het vragen van een grote dataset of het uitvoeren van veelvoudige verdere vragen kan de Notitie JupyterLab uit beschikbaar geheugen weglopen om het resulterende dataframe voorwerp op te slaan. Er zijn enkele indicatoren die in deze situatie zichtbaar zijn. Eerst, gaat de kernel de nutteloze staat in alhoewel de cel toont zoals die door het uitvoeren wordt vermeld [`*`] naast de cel. Bovendien geeft de onderste balk de hoeveelheid gebruikte/beschikbare RAM-geheugen aan.

![Beschikbaar ram](./images/jupyterlab/user-guide/allocate-ram.png)

Tijdens het lezen van de gegevens, kan het geheugen groeien tot het uw maximumhoeveelheid toegewezen geheugen bereikt. Het geheugen wordt vrijgemaakt zodra het maximale geheugen is bereikt en de kernel opnieuw wordt opgestart. Dit betekent het gebruikte geheugen in dit scenario als zeer laag kan tonen toe te schrijven aan het kernel opnieuw beginnen terwijl net vóór het nieuwe begin, het geheugen zeer dicht aan het maximum toegewezen RAM zou geweest zijn.

U lost dit probleem op door het tandwielpictogram rechtsboven in JupyterLab te selecteren en de schuifregelaar naar rechts te schuiven, gevolgd door **[!UICONTROL Update configs]** om meer RAM toe te wijzen. Bovendien, als u veelvoudige vragen in werking stelt en uw waarde van RAM het maximum toegewezen bedrag nadert, tenzij u de resultaten van vorige vragen nodig hebt, nieuw kernel om de beschikbare hoeveelheid RAM terug te stellen. Dit zorgt ervoor dat u de maximumhoeveelheid RAM beschikbaar aan de huidige vraag hebt.

![meer RAM toewijzen](./images/jupyterlab/user-guide/notebook-gpu-config.png)

In de gebeurtenis u de maximumhoeveelheid geheugen (RAM) toewijst en nog steeds deze kwestie ontmoet, kunt u uw vraag wijzigen om op een kleinere datasetgrootte te werken door de kolommen of de waaier van gegevens te verminderen. Als u de volledige hoeveelheid gegevens wilt gebruiken, kunt u het beste een Spark-laptop gebruiken.

## [!DNL JupyterLab] omgeving wordt niet geladen in [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dit probleem is opgelost, maar kan nog steeds voorkomen in de Google Chrome 80.x-browser. Controleer of uw Chrome-browser up-to-date is.

Met de [!DNL Google Chrome] browserversie 80.x, alle derdekoekjes worden geblokkeerd door gebrek. Dit beleid kan voorkomen [!DNL JupyterLab] vanaf het laden in Adobe Experience Platform.

Voer de volgende stappen uit om dit probleem op te lossen:

In uw [!DNL Chrome] browser, navigeer naar de rechterbovenhoek en selecteer **Instellingen** (U kunt ook &quot;chrome://settings/&quot; in de adresbalk kopiëren en plakken.) Blader vervolgens naar de onderkant van de pagina en klik op de knop **Geavanceerd** vervolgkeuzelijst.

![chroom geavanceerd](./images/faq/chrome-advanced.png)

De **Privacy en beveiliging** wordt weergegeven. Klik op Volgende **Site-instellingen** gevolgd door **Cookies en sitegegevens**.

![chroom geavanceerd](./images/faq/privacy-security.png)

![chroom geavanceerd](./images/faq/cookies.png)

Schakel ten slotte &quot;Cookies van derden blokkeren&quot; in op &quot;UIT&quot;.

![chroom geavanceerd](./images/faq/toggle-off.png)

>[!NOTE]
>
>U kunt cookies van derden ook uitschakelen en toevoegen [*.]ds.adobe.net naar de lijst van gewenste personen.

Ga naar &quot;chrome://flags/&quot; op de adresbalk. De vlag met de titel zoeken en uitschakelen *&quot;SameSite, standaard cookies&quot;* door het vervolgkeuzemenu aan de rechterkant te gebruiken.

![markering samensite uitschakelen](./images/faq/samesite-flag.png)

Na Stap 2, wordt u ertoe aangezet om uw browser opnieuw te lanceren. Nadat u het programma opnieuw hebt gestart, [!DNL Jupyterlab] moet toegankelijk zijn.

## Waarom heb ik geen toegang tot [!DNL JupyterLab] in Safari?

Safari schakelt cookies van derden standaard uit in Safari &lt; 12. Omdat [!DNL Jupyter] De instantie van de virtuele machine bevindt zich in een ander domein dan het bovenliggende frame. Adobe Experience Platform vereist momenteel dat cookies van derden zijn ingeschakeld. Schakel cookies van derden in of schakel over naar een andere browser, zoals [!DNL Google Chrome].

Voor Safari 12, moet u uw Agent van de Gebruiker aan &quot;[!DNL Chrome]&#39; of &#39;[!DNL Firefox]&quot;. Om uw Agent van de Gebruiker te schakelen, begin door te openen *Safari* en selecteert u **Voorkeuren**. Het voorkeurenvenster wordt weergegeven.

![Safari-voorkeuren](./images/faq/preferences.png)

Selecteer in het venster Safari-voorkeuren de optie **Geavanceerd**. Controleer vervolgens de *Ontwikkelmenu tonen in menubalk* doos. U kunt het voorkeurenvenster sluiten nadat deze stap is voltooid.

![Safari, geavanceerd](./images/faq/advanced.png)

Selecteer vervolgens op de bovenste navigatiebalk de optie **Ontwikkelen** -menu. Van binnen **Ontwikkelen** vervolgkeuzelijst, aanwijzen **Gebruikersagent**. U kunt de **[!DNL Chrome]** of **[!DNL Firefox]** Het koord van de Agent van de gebruiker u zou willen gebruiken.

![Ontwikkelen, menu](./images/faq/user-agent.png)

## Waarom zie ik een &#39;403 Verboden&#39; bericht als ik een bestand probeer te uploaden of te verwijderen in [!DNL JupyterLab]?

Als uw browser is ingeschakeld met software voor het blokkeren van advertenties, zoals [!DNL Ghostery] of [!DNL AdBlock] Bovendien moet het domein &quot;\*.adobe.net&quot; zijn toegestaan in elke advertentieblokkeringssoftware voor [!DNL JupyterLab] normaal te werken. Dit komt omdat [!DNL JupyterLab] virtuele machines worden uitgevoerd op een ander domein dan [!DNL Experience Platform] domein.

## Waarom doen sommige delen van mijn [!DNL Jupyter Notebook] zien er gescroleerd uit of niet renderen als code?

Dit kan gebeuren als de cel in kwestie per ongeluk van &quot;Code&quot;in &quot;Markdown&quot;wordt veranderd. Terwijl een codecel wordt geconcentreerd, die op de belangrijkste combinatie duwen **ESC+M** Hiermee wijzigt u het type cel in Markering. Het type van een cel kan worden gewijzigd door de vervolgkeuzelijst boven aan de laptop voor de geselecteerde cel(len). Als u een celtype in code wilt wijzigen, selecteert u eerst de cel die u wilt wijzigen. Klik vervolgens op het vervolgkeuzemenu dat het huidige type van de cel aangeeft en selecteer &quot;Code&quot;.

![](./images/faq/code_type.png)

## Hoe installeer ik aangepaste [!DNL Python] bibliotheken?

De [!DNL Python] kernel wordt vooraf geïnstalleerd met veel populaire bibliotheken voor machinetlering. U kunt echter aanvullende aangepaste bibliotheken installeren door de volgende opdracht in een codebel uit te voeren:

```shell
!pip install {LIBRARY_NAME}
```

Voor een volledige lijst met vooraf geïnstalleerde [!DNL Python] bibliotheken, zie [Bijlage, sectie van de gebruikershandleiding voor JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Kan ik aangepaste PySpark-bibliotheken installeren?

Helaas kunt u geen extra bibliotheken voor de PySpark-kernel installeren. U kunt echter contact opnemen met uw Adobe-medewerker van de klantenservice om aangepaste PySpark-bibliotheken voor u te laten installeren.

Voor een lijst met vooraf geïnstalleerde PySpark-bibliotheken raadpleegt u de [Bijlage, sectie van de gebruikershandleiding voor JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Is het mogelijk om te vormen [!DNL Spark] clusterbronnen voor [!DNL JupyterLab] [!DNL Spark] of PySpark kernel?

U kunt bronnen configureren door het volgende blok toe te voegen aan de eerste cel van uw laptop:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Voor meer informatie over [!DNL Spark] clustermiddelconfiguratie, met inbegrip van de volledige lijst configureerbare eigenschappen, zie [Gebruikershandleiding voor JupyterLab](./jupyterlab/overview.md#kernels).

## Waarom ontvang ik een fout wanneer het proberen bepaalde taken voor grotere datasets uitvoert?

Als u een fout ontvangt om een van de volgende redenen: `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Dit betekent doorgaans dat de bestuurder of een uitvoerder onvoldoende geheugen heeft. Bekijk de JupyterLab-laptops [gegevenstoegang](./jupyterlab/access-notebook-data.md) documentatie voor meer informatie over gegevensgrenzen en hoe te om taken op grote datasets uit te voeren. Deze fout kan meestal worden opgelost door het `mode` van `interactive` tot `batch`.

Bovendien, terwijl het schrijven van grote datasets Spark/PySpark, caching uw gegevens (`df.cache()`) voordat de schrijfcode wordt uitgevoerd, kan de prestaties aanzienlijk verbeteren.

<!-- remove this paragraph at a later date once the sdk is updated -->

Als u problemen ondervindt bij het lezen van gegevens en transformaties toepast op de gegevens, probeert u de gegevens vóór de transformaties in cache te plaatsen. Door uw gegevens in de cache te plaatsen, voorkomt u dat er meerdere leesbewerkingen in het netwerk plaatsvinden. Begin door de gegevens te lezen. Volgende, cache (`df.cache()`) de gegevens. Voer ten slotte een transformatie uit.

## Waarom duurt het zo lang voordat mijn Spark/PySpark notebooks gegevens lezen en schrijven?

Als u transformaties uitvoert op gegevens, zoals `fit()`, kunnen de transformaties meerdere keren worden uitgevoerd. Om de prestaties te verbeteren, kunt u uw gegevens in cache plaatsen met `df.cache()` voordat de `fit()`. Dit zorgt ervoor dat de transformaties slechts één keer worden uitgevoerd en verhindert veelvoudige lezing over het netwerk.

**Aanbevolen volgorde:** Begin door de gegevens te lezen. Voer vervolgens transformaties uit, gevolgd door caching (`df.cache()`) de gegevens. Ten slotte voert u een `fit()`.

## Waarom lopen mijn Spark/PySpark notebooks niet?

Als u een van de volgende fouten ontvangt:

- Taak afgebroken vanwege een fout in het werkgebied... RDD&#39;s met hetzelfde aantal elementen in elke partitie kunnen alleen worden gecomprimeerd.
- Externe RPC-client uitgeschakeld en andere geheugenfouten.
- Slechte prestaties bij het lezen en schrijven van datasets.

Controleer of de gegevens in de cache zijn opgeslagen (`df.cache()`) voordat de gegevens worden geschreven. Bij het uitvoeren van code in notebooks kunt u `df.cache()` vóór een handeling zoals `fit()` kan de prestaties van uw laptop aanzienlijk verbeteren. Gebruiken `df.cache()` alvorens een dataset te schrijven zorgt ervoor dat de transformaties slechts één keer in plaats van veelvoudige tijden worden uitgevoerd.

## [!DNL Docker Hub] limiteringsbeperkingen in de Data Science Workspace

Vanaf 20 november, 2020, gingen de tariefgrenzen voor anoniem en vrij voor authentiek verklaard gebruik van de Hub van de Dokker van kracht. Anoniem en gratis [!DNL Docker Hub] gebruikers kunnen maximaal 100 aanvragen om afbeeldingen elke zes uur in een container te laten teruggaan . Als deze wijzigingen op u van invloed zijn, ontvangt u het volgende foutbericht: `ERROR: toomanyrequests: Too Many Requests.` of `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Momenteel, zal deze grens slechts uw organisatie beïnvloeden als u probeert om 100 Notitieboekje aan Ontvangers binnen de periode van zes uur te bouwen of als u op Vonk gebaseerde Notities binnen de Werkruimte van de Wetenschap van Gegevens gebruikt die vaak omhoog en neer schrapt. Dit is echter onwaarschijnlijk, aangezien de cluster deze twee uur actief blijft voordat ze uitvallen. Hierdoor wordt het aantal vereiste pulls verminderd wanneer de cluster actief is. Als u een van de bovenstaande fouten ontvangt, moet u wachten tot uw [!DNL Docker] limit is reset.

Meer informatie over [!DNL Docker Hub] tarieflimieten, bezoek de [DockerHub-documentatie](https://www.docker.com/increase-rate-limits). Hieraan wordt gewerkt en in een volgende release wordt een oplossing verwacht.
