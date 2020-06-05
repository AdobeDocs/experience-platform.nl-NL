---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Samenwerken in JupyterLab met behulp van Git
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# Samenwerken in JupyterLab met behulp van Git

Git is een gedistribueerd versiecontrolesysteem voor het bijhouden van wijzigingen in broncode tijdens softwareontwikkeling. Git is vooraf geïnstalleerd in de JupyterLab-omgeving van de Data Science Workspace.

## Vereisten

>[!NOTE]
> De Git-server die u wilt gebruiken, moet via internet toegankelijk zijn.

De Data Science Workspace JupyterLab-omgeving is een gehoste omgeving en wordt niet geïmplementeerd binnen uw bedrijfsfirewall. Daarom moet de Git-server waarmee u verbinding maakt, toegankelijk zijn via het openbare internet. Dit zou een openbare of privé bewaarplaats op [GitHub](https://github.com/) of een ander geval van een server van het Git kunnen zijn die u hebt besloten om te ontvangen.

## Verbind Git met de Werkruimte van de Wetenschap van Gegevens JupyterLab Notitieomgeving

Start door te navigeren naar [!DNL Adobe Experience Platform] de omgeving voor [JupyterLabs-laptops](https://platform.adobe.com/notebooks/jupyterLab) .

Selecteer in JupyterLab de optie **[!UICONTROL Bestand]** en houd de muisaanwijzer boven **[!UICONTROL Nieuw]**. Van dropdown die verschijnt, uitgezochte **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Daarna, binnen *Terminal* navigeer aan uw werkruimte door het volgende bevel te gebruiken: `cd my-workspace`.

![cd-werkruimte](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
> Als u een lijst met beschikbare it-opdrachten wilt weergeven, geeft u de opdracht: `git -help` in uw terminal.

Vervolgens kloont u de opslagplaats die u wilt gebruiken met de `git clone` opdracht. Klonen van uw project met een `https://` URL in plaats van `ssh://`.

**Voorbeeld**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![klonen](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
> Om om het even welke schrijfverrichtingen (`git push` bijvoorbeeld) uit te voeren moeten de volgende configuratiebevelen voor elke nieuwe zitting worden in werking gesteld. Houd er ook rekening mee dat een pushopdracht vraagt om een gebruikersnaam en wachtwoord.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Volgende stappen

Nadat u klaar bent met het klonen van uw opslagplaats, kunt u Git gebruiken zoals u gewoonlijk op uw lokale computer zou doen om met anderen samen te werken aan laptops. Raadpleeg de gebruikershandleiding bij [JupyterLab voor meer informatie over wat u kunt doen in JupyterLab](./overview.md).
