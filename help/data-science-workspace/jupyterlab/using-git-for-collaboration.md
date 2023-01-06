---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;Git;Github
solution: Experience Platform
title: Samenwerken in JupyterLab met behulp van kit
type: Tutorial
description: Git is een gedistribueerd versiecontrolesysteem voor het bijhouden van wijzigingen in broncode tijdens softwareontwikkeling. Git is vooraf geïnstalleerd in de JupyterLab-omgeving van de Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Samenwerken in [!DNL JupyterLab] gebruiken [!DNL Git]

[!DNL Git] is een gedistribueerd versiecontrolesysteem voor het bijhouden van wijzigingen in broncode tijdens softwareontwikkeling. Git is vooraf geïnstalleerd in de [!DNL Data Science Workspace JupyterLab] milieu.

## Vereisten

>[!NOTE]
>
> De Git-server die u wilt gebruiken, moet via internet toegankelijk zijn.

De [!DNL Data Science Workspace JupyterLab] de omgeving is een gehoste omgeving en wordt niet geïmplementeerd binnen uw bedrijfsfirewall. Daarom moet de Git-server waarmee u verbinding maakt, toegankelijk zijn via het openbare internet. Dit kan een openbare of particuliere opslagplaats zijn op [GitHub](https://github.com/) of een andere instantie van een [!DNL Git] server die u zelf hebt gehost.

## Verbinden [!DNL Git] aan de [!DNL Data Science Workspace JupyterLab Notebooks] milieu

Starten met starten [!DNL Adobe Experience Platform] en naar de [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) milieu.

Within [!DNL JupyterLab], selecteert u **[!UICONTROL File]** dan boven **[!UICONTROL New]**. Selecteer in het vervolgkeuzemenu dat wordt weergegeven de optie **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Volgende, binnen *Terminal* navigeer aan uw werkruimte door het volgende bevel te gebruiken: `cd my-workspace`.

![cd-werkruimte](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Als u een lijst met beschikbare it-opdrachten wilt weergeven, geeft u de opdracht: `git -help` in uw terminal.

Vervolgens kloont u de opslagplaats die u wilt gebruiken met de `git clone` gebruiken. Uw project klonen met een `https://` URL in plaats van `ssh://`.

**Voorbeeld**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![klonen](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Om schrijfbewerkingen uit te voeren (`git push` bijvoorbeeld) de volgende configuratiebevelen moeten voor elke nieuwe zitting worden in werking gesteld. Houd er ook rekening mee dat een pushopdracht vraagt om een gebruikersnaam en wachtwoord.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Volgende stappen

Nadat u klaar bent met het klonen van uw opslagplaats, kunt u Git gebruiken zoals u gewoonlijk op uw lokale computer zou doen om met anderen samen te werken aan laptops. Voor meer informatie over wat u kunt doen binnen [!DNL JupyterLab], zie de [[!DNL JupyterLab user guide]](./overview.md).
