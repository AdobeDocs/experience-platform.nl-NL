---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;Git;Github
solution: Experience Platform
title: Samenwerken in JupyterLab met behulp van kit
type: Tutorial
description: Git is een gedistribueerd versiebeheersysteem voor het bijhouden van wijzigingen in broncode tijdens softwareontwikkeling. Git is vooraf geïnstalleerd in de Data Science Workspace JupyterLab-omgeving.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# Samenwerken in [!DNL JupyterLab] met [!DNL Git]

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

[!DNL Git] is een gedistribueerd versiebeheersysteem voor het bijhouden van wijzigingen in broncode tijdens softwareontwikkeling. Git wordt vooraf geïnstalleerd in de [!DNL Data Science Workspace JupyterLab] -omgeving.

## Vereisten

>[!NOTE]
>
> De Git-server die u wilt gebruiken, moet via internet toegankelijk zijn.

De [!DNL Data Science Workspace JupyterLab] -omgeving is een gehoste omgeving en wordt niet geïmplementeerd binnen uw bedrijfsfirewall. Daarom moet de Git-server waarmee u verbinding maakt, toegankelijk zijn via het openbare internet. Dit zou een openbare of privé bewaarplaats op [ GitHub ](https://github.com/) of een ander geval van een [!DNL Git] server kunnen zijn die u hebt beslist om te ontvangen.

## Verbind [!DNL Git] met het [!DNL Data Science Workspace JupyterLab Notebooks] milieu

Begin door [!DNL Adobe Experience Platform] te lanceren en aan het [[!DNL JupyterLabs Notebooks] ](https://platform.adobe.com/notebooks/jupyterLab) milieu te navigeren.

Selecteer in [!DNL JupyterLab] de optie **[!UICONTROL File]** en houd de muisaanwijzer boven **[!UICONTROL New]** . Selecteer **[!UICONTROL Terminal]** in het vervolgkeuzemenu dat wordt weergegeven.

![ JupyterLab Nav ](../images/jupyterlab/tutorials/open-terminal.png)

Daarna, binnen *Eind* navigeert aan uw werkruimte door het volgende bevel te gebruiken: `cd my-workspace`.

![ cd werkruimte ](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Als u een lijst met beschikbare it-opdrachten wilt zien, geeft u de opdracht `git -help` in de terminal uit.

Vervolgens kloont u de opslagplaats die u wilt gebruiken met de opdracht `git clone` . Klonen van uw project met een `https://` URL in plaats van `ssh://` .

**Voorbeeld**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![ kloon ](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Om schrijfbewerkingen uit te voeren (`git push` bijvoorbeeld), moeten de volgende configuratieopdrachten voor elke nieuwe sessie worden uitgevoerd. Houd er ook rekening mee dat een pushopdracht vraagt om een gebruikersnaam en wachtwoord.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Volgende stappen

Nadat u klaar bent met het klonen van uw opslagplaats, kunt u Git gebruiken zoals u gewoonlijk op uw lokale computer zou doen om met anderen samen te werken aan laptops. Zie [[!DNL JupyterLab user guide]](./overview.md) voor meer informatie over wat u kunt doen binnen [!DNL JupyterLab] .
