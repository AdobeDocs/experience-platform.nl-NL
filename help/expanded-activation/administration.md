---
title: Uitgebreid accountbeheer voor activering
description: Leer hoe u beheertaken kunt uitvoeren op uw uitgebreide activeringsaccount, zoals het controleren van het gebruik van licenties en het toewijzen van de juiste machtigingen.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---


# Accountbeheer

Als u een publiek van de Audience Manager wilt innemen en dit wilt activeren naar sociale en advertentiedoelen, moet u eerst een uitgebreide gebruikersaccount voor activering maken en het account toewijzen aan de juiste machtigingsrol.

Op deze pagina wordt uitgelegd hoe u een gebruikersaccount in de Admin Console maakt en de juiste machtigingen voor Uitgebreide activering toewijst.

## Gebruikersaccounts maken {#create-users}

Wat u moet doen [!DNL Audience Manager Expanded Activation], moet u een gebruikersaccount maken.

Een gebruikersaccount maken voor [!DNL Expanded Activation], volgt u de instructies voor het beheren van gebruikers van de [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/manage-users-individually.html) documentatie.

## Gebruikers toevoegen aan machtigingsrol {#permissions}

Nadat u een gebruikersaccount hebt gemaakt, moet u deze toevoegen aan de [!DNL Expanded Activation] machtigingsrol, in de [!DNL Expanded Activation] gebruikersinterface.

Ga naar **[!UICONTROL Administration]** -> **[!UICONTROL Permissions]** -> **[!UICONTROL Roles]** en selecteert u de **[!UICONTROL Expanded Activation Default Role]**.

![Uitgebreide afbeelding van de gebruikersinterface voor activering met de pagina Rollen.](assets/expanded-activation-role.png)

Ga naar de **[!UICONTROL Users]** en selecteert u **[!UICONTROL Add Users]**.

![Uitgebreide afbeelding van de gebruikersinterface voor activering die de pagina Gebruikers weergeeft.](assets/add-users.png)

Selecteer de nieuwe gebruiker in de beschikbare lijst en selecteer **[!UICONTROL Save]**.

![Uitgebreide afbeelding van de gebruikersinterface voor activering met de pagina Gebruikers toevoegen.](assets/add-user.png)

De gebruikersaccount wordt nu gemaakt en toegewezen aan de juiste rol. Het is nu klaar om toegang te krijgen tot **[!UICONTROL Expanded Activation]** gebruikersinterface.

## Licentiegebruik controleren {#license-usage}

Uw [!DNL Audience Manager Expanded Activation] Het contract bepaalt het maximum aantal gehashte e-mails dat je kunt invoeren voor je account.

U kunt deze informatie vinden door naar de **[!UICONTROL Administration]** -> **[!UICONTROL License Usage]** pagina.

![Uitgebreide afbeelding van de gebruikersinterface voor activering die het gebruiksscherm van de licentie weergeeft.](assets/license-usage.png)

Op deze pagina kunt u de volgende informatie vinden:

* **[!UICONTROL Product]**: Het Adobe product waarvoor u een licentie hebt. Dit zal altijd **[!UICONTROL Audience Manager Expanded Activation]**.
* **[!UICONTROL Primary metric]**: De naam van de metrische waarde die voor gebruik wordt bijgehouden. Dit zal altijd **[!UICONTROL Addressable audience]**.
* **[!UICONTROL License amount]**: Het maximum aantal gehashte e-mails dat u mag invoeren.

  >[!TIP]
  >
  >Je hebt gehakte e-mails via de [Audience Manager-bronaansluiting](../sources/connectors/adobe-applications/audience-manager.md). Zie de documentatie op [hoe te om publiek te activeren](activate-audiences.md) voor meer informatie .

* **[!UICONTROL Usage]**: Het aantal gehakte e-mails dat u hebt gegeten.
* **[!UICONTROL Usage %]**: het percentage van het licentiebedrag dat u hebt gebruikt.

Raadpleeg voor meer informatie over het gebruik van licenties in Experience Platform de [gebruiksdocumentatie voor licenties](../dashboards/guides/license-usage.md).

## Volgende stappen {#next-steps}

Nu u minstens één gebruikersaccount met de juiste toegang tot de uitgebreide activering hebt geconfigureerd, kunt u beginnen met het gebruik van het account voor [publiek activeren](activate-audiences.md).
