---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Handleiding voor het oplossen van problemen in de Data Science Workspace
topic: Troubleshooting
description: In dit document worden antwoorden gegeven op veelgestelde vragen over de Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 0%

---


# [!DNL Data Science Workspace] gids voor problemen

Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Data Science Workspace]. Raadpleeg de handleiding voor het oplossen van problemen met [!DNL Platform] Adobe Experience Platform API&#39;s in het algemeen voor vragen en het oplossen van problemen met betrekking tot API&#39;s [](../landing/troubleshooting.md).

## [!DNL JupyterLab] omgeving wordt niet geladen in [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dit probleem is opgelost, maar kan nog steeds voorkomen in de Google Chrome 80.x-browser. Controleer of uw Chrome-browser up-to-date is.

Met [!DNL Google Chrome] browserversie 80.x, worden alle derdekoekjes geblokkeerd door gebrek. Met dit beleid kan het laden [!DNL JupyterLab] in Adobe Experience Platform worden voorkomen.

Voer de volgende stappen uit om dit probleem op te lossen:

Navigeer in uw [!DNL Chrome] browser naar de rechterbovenhoek en selecteer **Instellingen** (u kunt ook &quot;chrome://settings/&quot; in de adresbalk kopiëren en plakken). Blader vervolgens naar de onderkant van de pagina en klik op het vervolgkeuzemenu **Geavanceerd** .

![chroom geavanceerd](./images/faq/chrome-advanced.png)

De sectie **Privacy en beveiliging** wordt weergegeven. Klik vervolgens op **Site-instellingen** gevolgd door **cookies en sitegegevens**.

![chroom geavanceerd](./images/faq/privacy-security.png)

![chroom geavanceerd](./images/faq/cookies.png)

Schakel ten slotte &quot;Cookies van derden blokkeren&quot; in op &quot;UIT&quot;.

![chroom geavanceerd](./images/faq/toggle-off.png)

>[!NOTE]
>
>U kunt cookies van derden uitschakelen en [* toevoegen.]ds.adobe.net naar de lijst van gewenste personen.

Ga naar &quot;chrome://flags/&quot; op de adresbalk. U kunt de markering *&quot;SameSite door standaardcookies&quot;* zoeken en uitschakelen in het vervolgkeuzemenu rechts.

![markering samensite uitschakelen](./images/faq/samesite-flag.png)

Na Stap 2, wordt u ertoe aangezet om uw browser opnieuw te lanceren. Nadat u de toepassing opnieuw hebt gestart, kunt u deze weer [!DNL Jupyterlab] gebruiken.

## Waarom heb ik geen toegang tot [!DNL JupyterLab] Safari?

Safari schakelt cookies van derden standaard uit in Safari &lt; 12. Aangezien de [!DNL Jupyter] virtuele-machinefunctie zich in een ander domein bevindt dan het bovenliggende frame, vereist Adobe Experience Platform momenteel dat cookies van derden zijn ingeschakeld. Schakel cookies van derden in of schakel over naar een andere browser, zoals [!DNL Google Chrome].

Voor Safari 12, moet u uw Agent van de Gebruiker op &quot;[!DNL Chrome]&quot;of &quot;[!DNL Firefox]&quot;schakelen. Om uw Agent van de Gebruiker te schakelen, begin door het menu van *Safari* te openen en **Voorkeur** te selecteren. Het voorkeurenvenster wordt weergegeven.

![Safari-voorkeuren](./images/faq/preferences.png)

Selecteer **Geavanceerd** in het voorkeurenvenster van Safari. Schakel vervolgens het menu Ontwikkelen *tonen in het vak van de menubalk* in. U kunt het voorkeurenvenster sluiten nadat deze stap is voltooid.

![Safari, geavanceerd](./images/faq/advanced.png)

Selecteer vervolgens in de bovenste navigatiebalk het menu **Ontwikkelen** . Houd de muisaanwijzer boven **Gebruikersagent** in het vervolgkeuzemenu **Ontwikkelen**. U kunt de tekenreeks **[!DNL Chrome]** **[!DNL Firefox]** of de tekenreeks Gebruikersagent selecteren die u wilt gebruiken.

![Ontwikkelen, menu](./images/faq/user-agent.png)

## Waarom zie ik een &#39;403 Verboden&#39; bericht wanneer ik een bestand probeer te uploaden of te verwijderen in [!DNL JupyterLab]?

Als uw browser is ingeschakeld met software voor het blokkeren van advertenties, zoals [!DNL Ghostery] of [!DNL AdBlock] Plus, moet het domein &quot;\*.adobe.net&quot; zijn toegestaan in elke software voor het blokkeren van advertenties, zodat [!DNL JupyterLab] deze normaal kan werken. Dit komt doordat [!DNL JupyterLab] virtuele machines op een ander domein dan het [!DNL Experience Platform] domein worden uitgevoerd.

## Waarom worden sommige onderdelen van mijn [!DNL Jupyter Notebook] uiterlijk gerasterd of niet gerenderd als code?

Dit kan gebeuren als de cel in kwestie per ongeluk van &quot;Code&quot;in &quot;Markdown&quot;wordt veranderd. Als u op de toetscombinatie **ESC+M** drukt terwijl een codecel de focus heeft, verandert het type cel in Markering. Het type van een cel kan worden gewijzigd door de vervolgkeuzelijst boven aan de laptop voor de geselecteerde cel(len). Als u een celtype in code wilt wijzigen, selecteert u eerst de cel die u wilt wijzigen. Klik vervolgens op het vervolgkeuzemenu dat het huidige type van de cel aangeeft en selecteer &quot;Code&quot;.

![](./images/faq/code_type.png)

## Hoe installeer ik aangepaste [!DNL Python] bibliotheken?

De [!DNL Python] kernel wordt vooraf geïnstalleerd met veel populaire bibliotheken voor computerleren. U kunt echter aanvullende aangepaste bibliotheken installeren door de volgende opdracht in een codebel uit te voeren:

```shell
!pip install {LIBRARY_NAME}
```

Voor een volledige lijst van vooraf geïnstalleerde [!DNL Python] bibliotheken, zie de [bijlage sectie van de Gids](./jupyterlab/overview.md#supported-libraries)van de Gebruiker JupyterLab.

## Kan ik aangepaste PySpark-bibliotheken installeren?

Helaas kunt u geen extra bibliotheken voor de PySpark-kernel installeren. U kunt echter contact opnemen met uw Adobe-medewerker van de klantenservice om aangepaste PySpark-bibliotheken voor u te laten installeren.

Voor een lijst van vooraf geïnstalleerde bibliotheken PySpark, zie de [bijlage sectie van de Gids](./jupyterlab/overview.md#supported-libraries)van de Gebruiker JupyterLab.

## Is het mogelijk om [!DNL Spark] clustermiddelen voor [!DNL JupyterLab] [!DNL Spark] of pySpark kernel te vormen?

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

Voor meer informatie over de configuratie van het [!DNL Spark] clustermiddel, met inbegrip van de volledige lijst van configureerbare eigenschappen, zie de [Gids](./jupyterlab/overview.md#kernels)van de Gebruiker JupyterLab.

## Waarom ontvang ik een fout wanneer het proberen bepaalde taken voor grotere datasets uitvoert?

Als er een fout optreedt om een `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` bepaalde reden, heeft het stuurprogramma of de uitvoerder onvoldoende geheugen. Zie de documentatie van de [gegevenstoegang](./jupyterlab/access-notebook-data.md) van Notitieboekjes JupyterLab voor meer informatie over gegevensgrenzen en hoe te om taken op grote datasets uit te voeren. Deze fout kan meestal worden opgelost door de `mode` instelling te wijzigen van `interactive` in `batch`.