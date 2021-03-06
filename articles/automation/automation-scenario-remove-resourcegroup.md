<properties
    pageTitle="De verwijdering van resourcegroepen automatiseren | Microsoft Azure"
    description="PowerShell Workflow-versie van een Azure Automation-scenario, inclusief runbooks om alle resourcegroepen in uw abonnement te verwijderen."
    services="automation"
    documentationCenter=""
    authors="MGoedtel"
    manager="jwhit"
    editor=""
    />
<tags
    ms.service="automation"
    ms.workload="tbd"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="get-started-article"
    ms.date="09/26/2016"
    ms.author="magoedte"/>


# Azure Automation-scenario: de verwijdering van resourcegroepen automatiseren

Veel klanten maken meer dan één resourcegroep. Sommige zijn voor het beheer van productietoepassingen en andere zijn bijvoorbeeld voor ontwikkelings-, test- en faseringsomgevingen. Het automatiseren van de implementatie van deze resources is één ding, maar om een resourcegroep buiten gebruik te stellen met een enkele muisklik is heel wat anders.  Automation is een perfect gebruiksscenario hiervoor en een uitstekende mogelijkheid om een dergelijke algemene beheertaak te stroomlijnen. Dit is ook handig als u werkt met een Azure-abonnement met een bestedingslimiet via een ledenaanbieding zoals MSDN of het programma Microsoft Partner Network Cloud Essentials. 

Dit scenario is gebaseerd op een PowerShell-runbook en is ontworpen om een of meer resourcegroepen die u opgeeft uit uw abonnement te verwijderen.  Het runbook biedt ondersteuning om eerst een test uit te voeren alvorens verder te gaan. Dit is de standaardwaarde.  Op deze manier voltooit u deze procedure zonder dat u het risico loopt dat u de resourcegroep per ongeluk verwijdert.   

## Het scenario ophalen

Dit scenario bestaat uit een PowerShell-runbook dat u uit de [PowerShell Gallery](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript) kunt downloaden. U kunt dit ook rechtstreeks vanuit de [Runbook Gallery](automation-runbook-gallery.md) in Azure Portal importeren.<br><br> 

Runbook | Beschrijving|
----------|------------|
Remove-ResourceGroup | Hiermee verwijdert u een of meer Azure-resourcegroepen en de daarbij behorende resources uit het abonnement.  
<br>
De volgende invoerparameters zijn voor dit runbook gedefinieerd:

Parameter | Beschrijving|
----------|------------|
NameFilter (vereist) | Hiermee kunt u een naamfilter opgeven, zodat u de resourcegroepen die u van plan bent te verwijderen, kunt beperken. U kunt meerdere waarden doorgeven met behulp van een met komma's gescheiden lijst.<br>Het filter is niet hoofdlettergevoelig en komt overeen met elke resourcegroep die de tekenreeks bevat.|
PreviewMode (optioneel) | Hiermee voert u het runbook uit om te zien welke resourcegroepen worden verwijderd, maar er wordt geen actie ondernomen.<br>De standaard is **waar**. Zo voorkomt u dat u onbedoeld een of meer resourcegroepen verwijdert die aan het runbook zijn doorgegeven.  

## Dit scenario installeren en configureren

### Vereisten

Dit runbook verifieert het gebruik van het [Azure Uitvoeren als-account](automation-sec-configure-azure-runas-account.md).    

### De runbooks installeren en publiceren

Nadat u het runbook hebt gedownload, kunt u dit importeren met behulp van de procedure in [Importing runbook procedures](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-Azure-Automation) (Procedures voor het importeren van runbooks).  Publiceer het runbook nadat dit is geïmporteerd in uw Automation-account.


## Het runbook gebruiken

De volgende stappen helpen u bij het uitvoeren van dit runbook. Zo raakt u vertrouwd met hoe het werkt.  In dit voorbeeld wordt het runbook alleen getest. De resourcegroep wordt niet daadwerkelijk verwijderd.  

1. Open uw Automation-account via Azure Portal en klik op de tegel **Runbooks**.
2. Selecteer het runbook **Remove-ResourceGroup** en klik op **Starten**.
3. Wanneer u het runbook start, wordt de blade **Runbook starten** geopend en kunt u de volgende waarden voor de parameters configureren.  Voer de naam van een of meer resourcegroepen in uw abonnement in waarmee u wilt testen en waarvan het niet erg is als deze per ongeluk worden verwijderd.<br> ![Remove-ResouceGroup-parameters](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)
    
    >[AZURE.NOTE] Zorg ervoor dat de optie **Previewmode** is ingesteld op **waar** om te voorkomen dat de geselecteerde resourcegroepen worden verwijderd.  ****Met dit runbook wordt de resourcegroep met het Automation-account dat dit runbook uitvoert niet verwijderd.  

4. Nadat u alle parameterwaarden hebt geconfigureerd, klikt u op **OK**. Het runbook wordt in de wachtrij geplaatst om te worden uitgevoerd.  

Als u de details van de runbooktaak **Remove-ResourceGroup** in Azure Portal wilt weergeven, selecteert u de tegel **Taken** van het runbook. Het taakoverzicht geeft de invoerparameters en de uitvoerstroom weer, naast algemene informatie over de taak en eventuele uitzonderingen.<br> ![Taakstatus van het runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Het **Taakoverzicht** bevat berichten van de uitvoer-, waarschuwings- en foutstromen. Selecteer de tegel **Uitvoer** om gedetailleerde resultaten van de uitvoering van het runbook weer te geven.<br> ![Uitvoerresultaten van het runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png) 

## Volgende stappen

- Zie [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md) (Een runbook in Azure Automation maken of importeren) om uw eigen runbook te maken
- Zie [Mijn eerste PowerShell Workflow-runbook](automation-first-runbook-textual.md) om aan de slag te gaan met PowerShell Workflow-runbooks


<!--HONumber=Sep16_HO4-->


