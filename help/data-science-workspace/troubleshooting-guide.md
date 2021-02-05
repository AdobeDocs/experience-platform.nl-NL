---
keywords: Experience Platform;problemen oplossen;Data Science Workspace;populaire onderwerpen
solution: Experience Platform
title: Handleiding voor probleemoplossing in de Data Science Workspace
topic: Troubleshooting
description: In dit document worden antwoorden gegeven op veelgestelde vragen over de Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 10ccccf72ff7a2fd726066332b9771dff1929af6
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---


# [!DNL Data Science Workspace] gids voor problemen

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Data Science Workspace]. Raadpleeg de [Adobe Experience Platform API-handleiding voor het oplossen van problemen](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot [!DNL Platform] API&#39;s in het algemeen.

## [!DNL JupyterLab] omgeving wordt niet geladen in  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dit probleem is opgelost, maar kan nog steeds voorkomen in de Google Chrome 80.x-browser. Controleer of uw Chrome-browser up-to-date is.

Met de browser [!DNL Google Chrome] versie 80.x, worden alle derdekoekjes geblokkeerd door gebrek. Dit beleid kan voorkomen dat [!DNL JupyterLab] in Adobe Experience Platform wordt geladen.

Voer de volgende stappen uit om dit probleem op te lossen:

Navigeer in uw [!DNL Chrome]-browser naar de rechterbovenhoek en selecteer **Instellingen** (u kunt ook &quot;chrome://settings/&quot; in de adresbalk kopiëren en plakken). Blader vervolgens naar de onderkant van de pagina en klik op het vervolgkeuzemenu **Geavanceerd**.

![chroom geavanceerd](./images/faq/chrome-advanced.png)

De sectie **Privacy en beveiliging** wordt weergegeven. Klik vervolgens op **Site-instellingen** gevolgd door **Cookies en sitegegevens**.

![chroom geavanceerd](./images/faq/privacy-security.png)

![chroom geavanceerd](./images/faq/cookies.png)

Schakel ten slotte &quot;Cookies van derden blokkeren&quot; in op &quot;UIT&quot;.

![chroom geavanceerd](./images/faq/toggle-off.png)

>[!NOTE]
>
>U kunt cookies van derden uitschakelen en [* toevoegen.]ds.adobe.net naar de lijst van gewenste personen.

Ga naar &quot;chrome://flags/&quot; op de adresbalk. U kunt de markering *&quot;SameSite door standaardcookies&quot;* zoeken en uitschakelen in het vervolgkeuzemenu rechts.

![markering samensite uitschakelen](./images/faq/samesite-flag.png)

Na Stap 2, wordt u ertoe aangezet om uw browser opnieuw te lanceren. Nadat u het programma opnieuw hebt gestart, is [!DNL Jupyterlab] toegankelijk.

## Waarom heb ik geen toegang tot [!DNL JupyterLab] in Safari?

Safari schakelt cookies van derden standaard uit in Safari &lt; 12. Aangezien uw [!DNL Jupyter] virtuele machine-instantie zich in een ander domein bevindt dan het bovenliggende frame, vereist Adobe Experience Platform momenteel dat cookies van derden zijn ingeschakeld. Schakel cookies van derden in of schakel over naar een andere browser, zoals [!DNL Google Chrome].

Voor Safari 12, moet u uw Agent van de Gebruiker op &quot;[!DNL Chrome]&quot;of &quot;[!DNL Firefox]&quot;schakelen. Om uw Agent van de Gebruiker te schakelen, begin door *Safari* menu te openen en **Voorkeur** te selecteren. Het voorkeurenvenster wordt weergegeven.

![Safari-voorkeuren](./images/faq/preferences.png)

Selecteer **Geavanceerd** in het venster Safari-voorkeuren. Schakel vervolgens het selectievakje *Ontwikkelen tonen in menubalk* in. U kunt het voorkeurenvenster sluiten nadat deze stap is voltooid.

![Safari, geavanceerd](./images/faq/advanced.png)

Selecteer vervolgens op de bovenste navigatiebalk het menu **Ontwikkelen**. Houd de muisaanwijzer boven **Gebruikersagent** in het vervolgkeuzemenu **Ontwikkelen**. U kunt de **[!DNL Chrome]** of **[!DNL Firefox]** koord van de Agent van de Gebruiker selecteren u zou willen gebruiken.

![Ontwikkelen, menu](./images/faq/user-agent.png)

## Waarom zie ik een &#39;403 Verboden&#39; bericht bij het uploaden of verwijderen van een bestand in [!DNL JupyterLab]?

Als uw browser is ingeschakeld met software voor het blokkeren van advertenties, zoals [!DNL Ghostery] of [!DNL AdBlock] Plus, moet het domein &quot;\*.adobe.net&quot; zijn toegestaan in elke software voor het blokkeren van advertenties om [!DNL JupyterLab] normaal te laten werken. Dit komt doordat virtuele machines [!DNL JupyterLab] op een ander domein dan [!DNL Experience Platform] domein in werking stellen.

## Waarom zien sommige delen van mijn [!DNL Jupyter Notebook] er anders uit of worden ze niet als code gerenderd?

Dit kan gebeuren als de cel in kwestie per ongeluk van &quot;Code&quot;in &quot;Markdown&quot;wordt veranderd. Als u op de toetscombinatie **ESC+M** drukt, verandert het type van de cel in Markdown als u op een codecel drukt. Het type van een cel kan worden gewijzigd door de vervolgkeuzelijst boven aan de laptop voor de geselecteerde cel(len). Als u een celtype in code wilt wijzigen, selecteert u eerst de cel die u wilt wijzigen. Klik vervolgens op het vervolgkeuzemenu dat het huidige type van de cel aangeeft en selecteer &quot;Code&quot;.

![](./images/faq/code_type.png)

## Hoe installeer ik aangepaste [!DNL Python] bibliotheken?

De [!DNL Python] kernel wordt vooraf geïnstalleerd met veel populaire bibliotheken voor machinetlering. U kunt echter aanvullende aangepaste bibliotheken installeren door de volgende opdracht in een codebel uit te voeren:

```shell
!pip install {LIBRARY_NAME}
```

Voor een volledige lijst van vooraf geïnstalleerde [!DNL Python] bibliotheken, zie [bijlage sectie van de Gids van de Gebruiker JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Kan ik aangepaste PySpark-bibliotheken installeren?

Helaas kunt u geen extra bibliotheken voor de PySpark-kernel installeren. U kunt echter contact opnemen met uw Adobe-medewerker van de klantenservice om aangepaste PySpark-bibliotheken voor u te laten installeren.

Voor een lijst van vooraf geïnstalleerde bibliotheken PySpark, zie [bijlage sectie van de Gids van de Gebruiker JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Is het mogelijk om [!DNL Spark] clustermiddelen voor [!DNL JupyterLab] [!DNL Spark] of PySpark kernel te vormen?

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

Voor meer informatie over [!DNL Spark] de configuratie van het clustermiddel, met inbegrip van de volledige lijst van configureerbare eigenschappen, zie [de Gids van de Gebruiker JupyterLab](./jupyterlab/overview.md#kernels).

## Waarom ontvang ik een fout wanneer het proberen bepaalde taken voor grotere datasets uitvoert?

Als u een fout ontvangt om een reden als `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Dit betekent doorgaans dat het stuurprogramma of de uitvoerder onvoldoende geheugen heeft. Zie de documentatie van JupyterLab Laptops [gegevenstoegang](./jupyterlab/access-notebook-data.md) voor meer informatie over gegevensgrenzen en hoe te om taken op grote datasets uit te voeren. Deze fout kan meestal worden opgelost door `mode` te wijzigen van `interactive` in `batch`.

## [!DNL Docker Hub] limiteringsbeperkingen in de Data Science Workspace

Vanaf 20 november, 2020, gingen de tariefgrenzen voor anoniem en vrij voor authentiek verklaard gebruik van de Hub van de Dokker van kracht. Gebruikers met anonieme en gratis [!DNL Docker Hub] kunnen maximaal 100 aanvragen indienen om de afbeelding elke zes uur opnieuw te laten ophalen. Als deze wijzigingen op u van invloed zijn, ontvangt u het volgende foutbericht: `ERROR: toomanyrequests: Too Many Requests.` of `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Momenteel, zal deze grens slechts uw organisatie beïnvloeden als u probeert om 100 Notitieboekje aan Ontvangers binnen de periode van zes uur te bouwen of als u op Vonk gebaseerde Notities binnen de Werkruimte van de Wetenschap van Gegevens gebruikt die vaak omhoog en neer schrapt. Dit is echter onwaarschijnlijk, aangezien de cluster deze twee uur actief blijft voordat ze uitvallen. Hierdoor wordt het aantal vereiste pulls verminderd wanneer de cluster actief is. Als u om het even welke bovengenoemde fouten ontvangt, zult u moeten wachten tot uw [!DNL Docker] grens wordt teruggesteld.

Voor meer informatie over [!DNL Docker Hub] tariefgrenzen, bezoek de [documentatie DockerHub](https://www.docker.com/increase-rate-limits). Hieraan wordt gewerkt en in een volgende release wordt een oplossing verwacht.