---
keywords: Experience Platform;problemen oplossen;Data Science Workspace;populaire onderwerpen
solution: Experience Platform
title: Workspace-gids voor probleemoplossing in gegevenswetenschappen
description: In dit document worden antwoorden gegeven op veelgestelde vragen over Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 0%

---

# [!DNL Data Science Workspace] gids voor probleemoplossing

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Data Science Workspace] . Voor vragen en het oplossen van problemen betreffende [!DNL Experience Platform] APIs in het algemeen, zie de [&#x200B; het oplossen van problemengids van Adobe Experience Platform API &#x200B;](../landing/troubleshooting.md).

## JupyterLab-laptopquerystatus zit vast in uitvoeringsstatus

Een JupyterLab-laptop geeft mogelijk aan dat een cel zich in de uitvoeringsstatus bevindt, voor onbepaalde tijd, in sommige gevallen onder onvoldoende geheugen. Bijvoorbeeld, wanneer het vragen van een grote dataset of het uitvoeren van veelvoudige verdere vragen kan de Notitie JupyterLab uit beschikbaar geheugen weglopen om het resulterende dataframe voorwerp op te slaan. Er zijn enkele indicatoren die in deze situatie zichtbaar zijn. Eerst wordt de kernel de status Niet-actief weergegeven, ook al wordt aangegeven dat de cel wordt uitgevoerd met het pictogram [`*`] naast de cel. Bovendien geeft de onderste balk de hoeveelheid gebruikte/beschikbare RAM-geheugen aan.

![&#x200B; Beschikbaar ram &#x200B;](./images/jupyterlab/user-guide/allocate-ram.png)

Tijdens het lezen van de gegevens, kan het geheugen groeien tot het uw maximumhoeveelheid toegewezen geheugen bereikt. Het geheugen wordt vrijgemaakt zodra het maximale geheugen is bereikt en de kernel opnieuw wordt opgestart. Dit betekent het gebruikte geheugen in dit scenario als zeer laag kan tonen toe te schrijven aan het kernel opnieuw beginnen terwijl net vóór het nieuwe begin, het geheugen zeer dicht aan het maximum toegewezen RAM zou geweest zijn.

U lost dit probleem op door het tandwielpictogram rechtsboven in JupyterLab te selecteren en de schuifregelaar naar rechts te schuiven, gevolgd door **[!UICONTROL Update configs]** om meer RAM-geheugen toe te wijzen. Bovendien, als u veelvoudige vragen in werking stelt en uw waarde van RAM het maximum toegewezen bedrag nadert, tenzij u de resultaten van vorige vragen nodig hebt, nieuw kernel om de beschikbare hoeveelheid RAM terug te stellen. Dit zorgt ervoor dat u de maximumhoeveelheid RAM beschikbaar aan de huidige vraag hebt.

![&#x200B; wijs meer grafiek &#x200B;](./images/jupyterlab/user-guide/notebook-gpu-config.png) toe

In de gebeurtenis u de maximumhoeveelheid geheugen (RAM) toewijst en nog steeds deze kwestie ontmoet, kunt u uw vraag wijzigen om op een kleinere datasetgrootte te werken door de kolommen of de waaier van gegevens te verminderen. Als u de volledige hoeveelheid gegevens wilt gebruiken, kunt u het beste een Spark-laptop gebruiken.

## [!DNL JupyterLab] -omgeving wordt niet geladen in [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dit probleem is opgelost, maar is mogelijk nog wel aanwezig in de Google Chrome 80.x-browser. Controleer of je Chrome-browser up-to-date is.

Met [!DNL Google Chrome] browser versie 80.x, worden alle derdekoekjes geblokkeerd door gebrek. Met dit beleid kan worden voorkomen dat [!DNL JupyterLab] wordt geladen in Adobe Experience Platform.

Voer de volgende stappen uit om dit probleem op te lossen:

In uw [!DNL Chrome] browser, navigeer aan top-right en selecteer **Montages** (alternatief kunt u &quot;chrome://settings/&quot;in de adresbar kopiëren en kleven). Daarna, scrol aan de bodem van de pagina en klik **Geavanceerde** dropdown.

![&#x200B; geavanceerd chroom &#x200B;](./images/faq/chrome-advanced.png)

De **privacy en veiligheid** sectie verschijnt. Daarna, klik op **montages van de Plaats** die door **Cookies en plaatsgegevens** worden gevolgd.

![&#x200B; geavanceerd chroom &#x200B;](./images/faq/privacy-security.png)

![&#x200B; geavanceerd chroom &#x200B;](./images/faq/cookies.png)

Schakel ten slotte &quot;Cookies van derden blokkeren&quot; in op &quot;UIT&quot;.

![&#x200B; geavanceerd chroom &#x200B;](./images/faq/toggle-off.png)

>[!NOTE]
>
>U kunt cookies van derden ook uitschakelen en [* toevoegen.] ds.adobe.net aan de lijst van gewenste personen.

Ga naar &quot;chrome://flags/&quot; op de adresbalk. Zoek naar en maak de vlag genoemd *&quot;SameSite door standaardkoekjes&quot;onbruikbaar* door het dropdown menu op het recht te gebruiken.

![&#x200B; maak de zelfde vlag &#x200B;](./images/faq/samesite-flag.png) onbruikbaar

Na Stap 2 wordt u gevraagd uw browser opnieuw te starten. Nadat u de toepassing opnieuw hebt gestart, is [!DNL Jupyterlab] toegankelijk.

## Waarom heb ik geen toegang tot [!DNL JupyterLab] in Safari?

Safari schakelt cookies van derden standaard uit in Safari &lt; 12. Aangezien de instantie van de [!DNL Jupyter] virtuele machine zich in een ander domein bevindt dan het bovenliggende frame, vereist Adobe Experience Platform momenteel dat cookies van derden zijn ingeschakeld. Schakel cookies van derden in of schakel over naar een andere browser, zoals [!DNL Google Chrome] .

Voor Safari 12, moet u uw Agent van de Gebruiker op &quot;[!DNL Chrome]&quot;of &quot;[!DNL Firefox]&quot;schakelen. Om uw Agent van de Gebruiker te schakelen, begin door het *Safari* menu te openen en **Voorkeur** te selecteren. Het voorkeurenvenster wordt weergegeven.

![&#x200B; voorkeur Safari &#x200B;](./images/faq/preferences.png)

Binnen het de voorkeurenvenster van Safari, uitgezochte **Geavanceerd**. Dan controleer *tonen ontwikkelt menu in menubar* doos. U kunt het voorkeurenvenster sluiten nadat deze stap is voltooid.

![&#x200B; Geavanceerde Safari &#x200B;](./images/faq/advanced.png)

Daarna, van de hoogste navigatiebar selecteren **ontwikkelt** menu. Van binnen **ontwikkel** dropdown, beweeg over **Agent van de Gebruiker**. U kunt de tekenreeks **[!DNL Chrome]** of **[!DNL Firefox]** Gebruikersagent selecteren die u wilt gebruiken.

![&#x200B; ontwikkelt menu &#x200B;](./images/faq/user-agent.png)

## Waarom zie ik een &#39;403 Verboden&#39; bericht als ik een bestand probeer te uploaden of te verwijderen in [!DNL JupyterLab] ?

Als uw browser is ingeschakeld met software voor het blokkeren van advertenties, zoals [!DNL Ghostery] of [!DNL AdBlock] Plus, moet het domein &quot;\*.adobe.net&quot; zijn toegestaan in elke software voor het blokkeren van advertenties, anders werkt [!DNL JupyterLab] niet naar behoren. Dit komt omdat [!DNL JupyterLab] virtuele machines op een ander domein dan het [!DNL Experience Platform] domein worden uitgevoerd.

## Waarom zien sommige delen van mijn [!DNL Jupyter Notebook] er gescroleerd uit of worden ze niet weergegeven als code?

Dit kan gebeuren als de cel in kwestie per ongeluk van &quot;Code&quot;in &quot;Markdown&quot;wordt veranderd. Terwijl een codecel wordt geconcentreerd, verandert het drukken van de belangrijkste combinatie **ESC+M** het type van de cel in Markering. Het type van een cel kan worden gewijzigd door de vervolgkeuzelijst boven aan de laptop voor de geselecteerde cel(len). Als u een celtype in code wilt wijzigen, selecteert u eerst de cel die u wilt wijzigen. Klik vervolgens op het vervolgkeuzemenu dat het huidige type van de cel aangeeft en selecteer &quot;Code&quot;.

![](./images/faq/code_type.png)

## Hoe installeer ik aangepaste [!DNL Python] bibliotheken?

De [!DNL Python] kernel wordt vooraf geïnstalleerd met veel populaire bibliotheken voor machinetlering. U kunt echter aanvullende aangepaste bibliotheken installeren door de volgende opdracht in een codebel uit te voeren:

```shell
!pip install {LIBRARY_NAME}
```

Voor een volledige lijst van vooraf geïnstalleerde [!DNL Python] bibliotheken, zie de [&#x200B; appendix sectie van de Gids van de Gebruiker JupyterLab &#x200B;](./jupyterlab/overview.md#supported-libraries).

## Kan ik aangepaste PySpark-bibliotheken installeren?

Helaas kunt u geen extra bibliotheken voor de PySpark-kernel installeren. U kunt echter contact opnemen met uw Adobe-medewerker van de klantenservice om aangepaste PySpark-bibliotheken voor u te laten installeren.

Voor een lijst van vooraf geïnstalleerde bibliotheken PySpark, zie de [&#x200B; bijlage sectie van de Gids van de Gebruiker JupyterLab &#x200B;](./jupyterlab/overview.md#supported-libraries).

## Is het mogelijk om [!DNL Spark] clusterbronnen voor [!DNL JupyterLab] [!DNL Spark] of PySpark kernel te configureren?

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

Voor meer informatie over [!DNL Spark] configuratie van het clustermiddel, met inbegrip van de volledige lijst van configureerbare eigenschappen, zie de [&#x200B; Gids van de Gebruiker JupyterLab &#x200B;](./jupyterlab/overview.md#kernels).

## Waarom ontvang ik een fout wanneer het proberen bepaalde taken voor grotere datasets uitvoert?

Als u een fout ontvangt om een reden als `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` , heeft dit doorgaans tot gevolg dat het geheugen van het stuurprogramma of de uitvoerder bijna vol is. Zie de JupyterLab Notitieboekjes [&#x200B; gegevenstoegang &#x200B;](./jupyterlab/access-notebook-data.md) documentatie voor meer informatie over gegevensgrenzen en hoe te om taken op grote datasets uit te voeren. Deze fout kan meestal worden opgelost door de `mode` van `interactive` in `batch` te wijzigen.

Bovendien, terwijl het schrijven van grote datasets Spark/PySpark, caching van uw gegevens (`df.cache()`) alvorens schrijven code uit te voeren kan prestaties zeer verbeteren.

<!-- remove this paragraph at a later date once the sdk is updated -->

Als u problemen ondervindt bij het lezen van gegevens en transformaties toepast op de gegevens, probeert u de gegevens vóór de transformaties in cache te plaatsen. Door uw gegevens in de cache te plaatsen, voorkomt u dat er meerdere leesbewerkingen in het netwerk plaatsvinden. Begin door de gegevens te lezen. Plaats vervolgens de gegevens in de cache (`df.cache()`). Voer ten slotte een transformatie uit.

## Waarom duurt het zo lang voordat mijn Spark/PySpark notebooks gegevens lezen en schrijven?

Als u transformaties uitvoert op gegevens, zoals met `fit()` , kunnen de transformaties meerdere keren worden uitgevoerd. Als u de prestaties wilt verbeteren, plaatst u de gegevens in de cache met `df.cache()` voordat u de `fit()` uitvoert. Dit zorgt ervoor dat de transformaties slechts één keer worden uitgevoerd en verhindert veelvoudige lezing over het netwerk.

**geadviseerde orde:** Begin door de gegevens te lezen. Daarna, voer transformaties uit die door caching (`df.cache()`) worden gevolgd de gegevens. Voer ten slotte een `fit()` uit.

## Waarom lopen mijn Spark/PySpark notebooks niet?

Als u een van de volgende fouten ontvangt:

- Taak afgebroken vanwege een fout in het werkgebied... Kan alleen RDD&#39;s met hetzelfde aantal elementen in elke partitie comprimeren.
- Externe RPC-client uitgeschakeld en andere geheugenfouten.
- Slechte prestaties bij het lezen en schrijven van datasets.

Controleer of u de gegevens in de cache plaatst (`df.cache()`) voordat u de gegevens schrijft. Bij het uitvoeren van code in notebooks kan het gebruik van `df.cache()` vóór een handeling als `fit()` de prestaties van een laptop aanzienlijk verbeteren. Als u `df.cache()` gebruikt voordat u een gegevensset schrijft, weet u zeker dat de transformaties slechts één keer worden uitgevoerd in plaats van meerdere keren.

## [!DNL Docker Hub] beperkingen beperken in Data Science Workspace

Vanaf 20 november, 2020, gingen de tariefgrenzen voor anoniem en vrij voor authentiek verklaard gebruik van de Hub van de Dokker van kracht. Gebruikers met anonieme of gratis [!DNL Docker Hub] zijn beperkt tot 100 aanvragen om de afbeelding elke zes uur opnieuw te laten ophalen. Als deze wijzigingen gevolgen hebben, ontvangt u het volgende foutbericht: `ERROR: toomanyrequests: Too Many Requests.` of `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.` .

Momenteel, zal deze grens slechts uw organisatie beïnvloeden als u probeert om 100 Notitieboekje aan Ontvangers binnen de periode van zes uur te bouwen of als u op Vonk gebaseerde Notities binnen de Wetenschap van Gegevens Workspace gebruikt die vaak omhoog en neer schrapen. Dit is echter onwaarschijnlijk, aangezien de cluster deze twee uur actief blijft voordat ze uitvallen. Hierdoor wordt het aantal vereiste pulls verminderd wanneer de cluster actief is. Als u een van de bovenstaande fouten ontvangt, moet u wachten tot de limiet van [!DNL Docker] opnieuw is ingesteld.

Voor meer informatie over [!DNL Docker Hub] tariefgrenzen, bezoek de [&#x200B; documentatie DockerHub &#x200B;](https://www.docker.com/increase-rate-limits). Hieraan wordt gewerkt en in een volgende release wordt een oplossing verwacht.
