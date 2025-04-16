# 03_CLI_+_Storage
### IBM Cloud CLI lokal nutzen

- Um die IBM Cloud CLI lokal zu nutzen öffnen Sie ihr Terminal und führen Sie das folgendee Skirpt je nach Betriebssystem aus: 

    - MacOS: ``curl -fsSL https://clis.cloud.ibm.com/install/osx | sh``
    - Linux: ``curl -fsSL https://clis.cloud.ibm.com/install/linux | sh``
    - Windows: ``iex (New-Object Net.WebClient).DownloadString('https://clis.cloud.ibm.com/install/powershell')``
        - Wenn Sie bei der Windows Installation  auf Fehler wie " The underlying connection was closed: An unexpected error occurred on a send stoßen, stellen Sie sicher, dass Sie .Net Framework 4.5 oder höher installiert haben. Versuchen Sie außerdem, das TLS 1.2-Protokoll durch Ausführen des folgenden Befehls zu aktivieren: 
        ``[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12``

- nach erfolgreicher Installation könenn Sie sich mit dem Befehl``ibmcloud login`` an Ihrem Account anmelden
    -  sollten Sie beim versuch der Anmeldung einen Fehler erhalten wie ***Sie verwenden eine eingebundene Benutzer-ID; verwenden Sie einen Einmalkenncode ( ibmcloud login --sso ) oder einen API-Schlüssel ( ibmcloud login --apikey key or @key_file ) zur Authentifizierung.*** , dann holen Sie sich ihren Einmalkenncode im IBM Cloud Portal.
        - Den Einmalkenncode zu Anmeldung in der CLI finden Sie wenn sie oben in der Navigationsbar ganz rechts in der Ecke auf das Profilicon klicken und danach ``Log in to CLI and API`` klicken, kopieren Sie jetzt nurnoch den Loginbefehl für die IBM Cloud CLI heraus und pasten Ihn in ihr Terminal.
        - Sie sollten nun lokal über die CLI in ihrem Account sein  

<img src="_images/CLI_login.png" width="700">

>[!TIP]
> Um immer die neuste Version der CLI zu nutzen führen Sie den Befehl ``ibmcloud update`` aus
>
> Die aktuelle Version Ihrer CLI finden Sie über ``ibmcloud -v`` heraus

- Da wir mit PowerVS arbeiten möchten brauchen wir für unsere CLI noch ein Plugin
- Das Power-IaaS Plugin installieren wir über den Befehl ``ibmcloud plugin install power-iaas```

>[!NOTE]
> Eine Liste aller Plugins finden Sie über ``ibmcloud plugin repo-plugins``
>
> Um Ihre bereits installieren Plugins aufzulisten nutzen Sie ``ibmcloud plugin list``
>
> Um Plugins zu aktualisieren nutzen Sie ``ibmcloud plugin update``

>[!NOTE]
> Weitere Infos über die IBM Cloud CLI finden Sie in der offiziellen Dokumentation: [IBM Cloud-CLI](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli)