# 03_CLI_+_Storage
### IBM Cloud-CLI lokal nutzen

- Um die IBM Cloud CLI lokal zu nutzen öffnen Sie ihr Terminal und führen Sie das folgende Skript je nach Betriebssystem aus: 

    - MacOS: ``curl -fsSL https://clis.cloud.ibm.com/install/osx | sh``
    - Linux: ``curl -fsSL https://clis.cloud.ibm.com/install/linux | sh``
    - Windows: ``iex (New-Object Net.WebClient).DownloadString('https://clis.cloud.ibm.com/install/powershell')``
        - Wenn Sie bei der Windows Installation  auf Fehler wie " The underlying connection was closed: An unexpected error occurred on a send stoßen, stellen Sie sicher, dass Sie .Net Framework 4.5 oder höher installiert haben. Versuchen Sie außerdem, das TLS 1.2-Protokoll durch Ausführen des folgenden Befehls zu aktivieren: 
        ``[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12``

- Nach erfolgreicher Installation könenn Sie sich mit dem Befehl``ibmcloud login`` an Ihrem Account anmelden
    -  Sollten Sie beim versuch der Anmeldung einen Fehler erhalten wie ***Sie verwenden eine eingebundene Benutzer-ID; verwenden Sie einen Einmalkenncode ( ibmcloud login --sso ) oder einen API-Schlüssel ( ibmcloud login --apikey key or @key_file ) zur Authentifizierung.*** , dann holen Sie sich ihren Einmalkenncode im IBM Cloud Portal.
       - Den Einmalkenncode zur Anmeldung in der CLI finden Sie, indem Sie oben in der Navigationsleiste ganz rechts auf das Profil-Icon klicken und anschließend auf ``Log in to CLI and API`` gehen. Kopieren Sie nun den Login-Befehl für die IBM Cloud CLI und fügen Sie ihn in Ihr Terminal ein. 
       - Sie sollten nun lokal über die CLI in Ihrem Account angemeldet sein.

<img src="_images/CLI_login.png" width="700">

>[!TIP]
> Um immer die neuste Version der CLI zu nutzen führen Sie den Befehl ``ibmcloud update`` aus
>
> Die aktuelle Version Ihrer CLI finden Sie über ``ibmcloud -v`` heraus

- Da wir mit PowerVS arbeiten möchten brauchen wir für unsere CLI noch ein Plugin
- Das Power-IaaS Plugin installieren wir über den Befehl ``ibmcloud plugin install power-iaas``

>[!NOTE]
> Eine Liste aller Plugins finden Sie über ``ibmcloud plugin repo-plugins``
>
> Um Ihre bereits installieren Plugins aufzulisten nutzen Sie ``ibmcloud plugin list``
>
> Um Plugins zu aktualisieren nutzen Sie ``ibmcloud plugin update``

>[!NOTE]
> Weitere Infos über die IBM Cloud CLI finden Sie in der offiziellen Dokumentation: [IBM Cloud-CLI](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli)

---
### IBM Cloud-CLI im GUI

- Es ist natürlich auch möglich die IBM Cloud CLI im IBM Cloud Portal zu nutzen, wählen sie dafür oben in der Navigationsbar das Icon aus welches wie ein Terminal aussieht und starten Sie per Klick eine neue Cloud Shell

<img src="_images/Cloud-Shell.png" width="700">

- Sie können jetzt direkt mit der IBM Cloud CLI interagieren, tippen Sie beispielweise ``ibmcloud help`` ein um Hilfe zu bekommen 
- Testen Sie den Befehl ``ibmcloud plugin list``, sie sehen dass in der Cloud Shell bereits alle Plugins installiert sind

>[!NOTE]
> Um sich mit allgemeinen Befehlen der IBM Cloud-CLI bekannt zu machen schauen sie in die offizielle Dokumentation über diesen Link: [IBM Cloud-CLI (ibmcloud) Befehle ](https://cloud.ibm.com/docs/cli?topic=cli-ibmcloud_cli) 

---

### Arbeiten mir PowerVS in der IBM Cloud per CLI

#### Basics

- Hilfe aufrufen: ``ibmcloud pi help``

>[!IMPORTANT]
> Stellen sie sicher, dass Sie das Power-IaaS Plugin installiert haben falls Sie auf der CLI lokal arbeiten
>
> ``ibmcloud plugin install power-iaas``

- Vorhandene Workspaces auflisten: ``ibmcloud pi ws list``
- Einen Workspaces als Target für folgende Befehle auswählen: ``ibmcloud pi target <CRN>``
    - Ihre CRN finden sie beim auflisten der Workspaces heraus

#### Instanz Snapshot aufnehmen

- Nachdem Sie Ihren Workspace als Target ausgewählt haben listen Sie alle verfügbaren Instanzen im Workspace auf mit dem Befehl: ``ibmcloud pi ins``


#### Instanz Volume clonen