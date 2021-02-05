---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;Git;Github
solution: Experience Platform
title: Samenwerken in JupyterLab met behulp van kit
topic: tutorial
type: Tutorial
description: Git is een gedistribueerd versiecontrolesysteem voor het bijhouden van wijzigingen in broncode tijdens softwareontwikkeling. Git is vooraf geïnstalleerd in de JupyterLab-omgeving van de Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---


# Samenwerken in [!DNL JupyterLab] met [!DNL Git]

[!DNL Git] is een gedistribueerd versiecontrolesysteem voor het bijhouden van wijzigingen in broncode tijdens softwareontwikkeling. Git wordt vooraf geïnstalleerd in de [!DNL Data Science Workspace JupyterLab]-omgeving.

## Vereisten

>[!NOTE]
>
> De Git-server die u wilt gebruiken, moet via internet toegankelijk zijn.

De [!DNL Data Science Workspace JupyterLab]-omgeving is een gehoste omgeving en wordt niet geïmplementeerd binnen uw bedrijfsfirewall. Daarom moet de Git-server waarmee u verbinding maakt, toegankelijk zijn via het openbare internet. Dit zou een openbare of privé bewaarplaats op [GitHub](https://github.com/) of een ander geval van een [!DNL Git] server kunnen zijn die u hebt besloten om zich te ontvangen.

## [!DNL Git] verbinden met de [!DNL Data Science Workspace JupyterLab Notebooks]-omgeving

Start door [!DNL Adobe Experience Platform] te starten en naar de [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)-omgeving te navigeren.

Selecteer **[!UICONTROL Bestand]** in [!DNL JupyterLab] en houd de muisaanwijzer boven **[!UICONTROL Nieuw]**. Van dropdown die verschijnt, selecteer **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Daarna, binnen *Terminal* navigeer aan uw werkruimte door het volgende bevel te gebruiken: `cd my-workspace`.

![cd-werkruimte](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Als u een lijst met beschikbare it-opdrachten wilt weergeven, geeft u de opdracht: `git -help` binnen uw Terminal.

Vervolgens kloont u de opslagplaats die u wilt gebruiken met de opdracht `git clone`. U kunt uw project klonen met een `https://`-URL in plaats van `ssh://`.

**Voorbeeld**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![klonen](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Om om het even welke schrijfverrichtingen (`git push` bijvoorbeeld) uit te voeren moeten de volgende configuratiebevelen voor elke nieuwe zitting worden in werking gesteld. Houd er ook rekening mee dat een pushopdracht vraagt om een gebruikersnaam en wachtwoord.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Volgende stappen

Nadat u klaar bent met het klonen van uw opslagplaats, kunt u Git gebruiken zoals u gewoonlijk op uw lokale computer zou doen om met anderen samen te werken aan laptops. Voor meer informatie over wat u binnen [!DNL JupyterLab] kunt doen, zie [[!DNL JupyterLab user guide]](./overview.md).
