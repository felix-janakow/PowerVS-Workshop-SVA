# 03_CLI_+_Storage
### IBM Cloud-CLI lokal nutzen

- Um die IBM Cloud-CLI lokal zu nutzen öffnen Sie ihr Terminal und führen Sie das folgende Skript je nach Betriebssystem aus: 

    - MacOS: ``curl -fsSL https://clis.cloud.ibm.com/install/osx | sh``
    - Linux: ``curl -fsSL https://clis.cloud.ibm.com/install/linux | sh``
    - Windows: ``iex (New-Object Net.WebClient).DownloadString('https://clis.cloud.ibm.com/install/powershell')``
        - Wenn Sie bei der Windows Installation  auf Fehler wie " The underlying connection was closed: An unexpected error occurred on a send stoßen, stellen Sie sicher, dass Sie .Net Framework 4.5 oder höher installiert haben. Versuchen Sie außerdem, das TLS 1.2-Protokoll durch Ausführen des folgenden Befehls zu aktivieren: 
        ``[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12``

- Nach erfolgreicher Installation könenn Sie sich mit dem Befehl``ibmcloud login`` an Ihrem Account anmelden
    -  Sollten Sie beim Versuch der Anmeldung einen Fehler erhalten wie ***Sie verwenden eine eingebundene Benutzer-ID; verwenden Sie einen Einmalkenncode ( ibmcloud login --sso ) oder einen API-Schlüssel ( ibmcloud login --apikey key or @key_file ) zur Authentifizierung.*** , dann holen Sie sich ihren **Einmalkenncode** im IBM Cloud Portal.
       - Den Einmalkenncode zur Anmeldung in der CLI finden Sie, indem Sie oben in der Navigationsleiste ganz rechts auf das Profil-Icon klicken und anschließend auf ``Log in to CLI and API`` gehen. Kopieren Sie nun den Login-Befehl für die IBM Cloud-CLI und fügen Sie diesen in Ihr Terminal ein. 
       - Sie sollten nun lokal über die CLI in Ihrem Account angemeldet sein

<img src="_images/CLI_login.png" width="700">

>[!TIP]
> - Um immer die neuste Version der CLI zu nutzen führen Sie den Befehl ``ibmcloud update`` aus
>-  Die aktuelle Version Ihrer CLI finden Sie über ``ibmcloud -v`` heraus

- Da wir mit PowerVS arbeiten möchten brauchen wir für unsere CLI noch ein Plugin
- Das Power-IaaS Plugin installieren wir über den Befehl ``ibmcloud plugin install power-iaas``

>[!NOTE]
> - Eine Auflistung aller Plugins finden Sie über ``ibmcloud plugin repo-plugins``
> - Um Ihre bereits installieren Plugins aufzulisten nutzen Sie ``ibmcloud plugin list``
> - Um Plugins zu aktualisieren nutzen Sie ``ibmcloud plugin update``

>[!NOTE]
> Weitere Infos über die IBM Cloud-CLI finden Sie in der offiziellen Dokumentation: [IBM Cloud-CLI](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli)

---
### IBM Cloud-CLI im GUI

- Es ist natürlich auch möglich die IBM Cloud-CLI im IBM Cloud Portal zu nutzen, wählen Sie dafür oben in der Navigationsbar das Icon aus, welches wie ein Terminal aussieht und starten Sie per Klick eine neue Cloud Shell

<img src="_images/Cloud-Shell.png" width="700">

- Sie können jetzt direkt mit der IBM Cloud-CLI interagieren, tippen Sie beispielsweise ``ibmcloud help`` ein um Hilfe zu bekommen 
- Testen Sie den Befehl ``ibmcloud plugin list``, Sie sehen dass in der Cloud Shell bereits alle Plugins installiert sind

>[!TIP]
> In der Cloud Shell müssen Sie nicht für jeden Befehl zuerst ``ibmcloud`` eintippen, es reicht wenn Sie die Befehle nur mit ``ic``eingeben
> - Sie könnten sich um mit ``ic``auch lokal arbeiten zu können ein "Alias" in ihre Shell Konfigurationsdatei (z.b ~/.zshrc für MacOS) setzen


>[!NOTE]
> Um sich mit allgemeinen Befehlen der IBM Cloud-CLI bekannt zu machen werfen Sie einen Blick in die offizielle Dokumentation: [IBM Cloud-CLI (ibmcloud) Befehle ](https://cloud.ibm.com/docs/cli?topic=cli-ibmcloud_cli) 

---

### Arbeiten mir PowerVS in der IBM Cloud per CLI

>[!NOTE]
> Sollten Sie im folgenden Teil des Workshops mit den verschiedenen Befehlen und IDs durcheinanderkommen, nutzen Sie das Dokument Mini_Cheat_Sheet.md im Workshop-Repository für eine bessere Übersicht über die CLI-Commands.

### Basics

- Hilfe aufrufen: ``ibmcloud pi help``

>[!IMPORTANT]
> Stellen Sie sicher, dass Sie das Power-IaaS Plugin installiert haben falls Sie auf der CLI lokal arbeiten
>
> ``ibmcloud plugin install power-iaas``

- Vorhandene Workspaces auflisten: ``ibmcloud pi ws list``
- Einen Workspaces als Target für folgende Befehle auswählen: ``ibmcloud pi ws target <CRN>``
    - Ihre CRN finden sie beim auflisten der Workspaces heraus

---
### Vorbereitungen für Snapshots

- Nachdem Sie Ihren Workspace als Target ausgewählt haben listen Sie alle verfügbaren Instanzen im Workspace auf mit dem Befehl: ``ibmcloud pi ins ls``
    - Wenn Sie in der Zwischenzeit keine weiteren Instanzen in Ihrem Workspace angelegt haben sollte nur die Instanz sichtbar sein, die Sie in **Teil 01** des Workshops erstellt haben
- Kopieren Sie die **ID** der Instanz und legen Sie sie griffbereit ab, da wir die ID im Anschluss benötigen
- Greifen Sie auf weitere Informationen der Instanz zu mit dem Befehl ``ibmcloud pi ins get <ID>``
- Neben **Datenträger** sollten Sie jetzt 2 ID`s sehen wenn Sie in **Teil 02 - Volume hinzufügen** ein weiter Volume an die LPAR gehängt haben
- Kopieren Sie die **ID** des Datenträgers, der im Workshop Teil 02_LPAR_Management manuell erstellt wurde, und legen Sie diese griffbereit ab, da wir die ID im Anschluss benötigen


<img src="_images/ibmcloud_pi_ins_get.png" width="850">

> [!TIP]
> Um im Portal rauszufinden welche ID zu welchem bestimmten Volume gehört, navigieren Sie über **Storage volumes** auf Ihr Volume, hier sollten Sie die ID sehen
>
> <img src="_images/storage_volumes.png" width="700">
>
> Um in der CLI die ID eines Volumes rauzfinden nutzen Sie den Befehl: ``ibmcloud pi vol ls``

---
#### Snapshot von Instanz + Volume erstellen

- Kreiren Sie einen Snaphot der Instanz + Volume mit dem Befehl ``ibmcloud pi ins snap cr <ID_Instanz> --name <wählen_sie_einen_Namen> --volumes <ID_Volume>``

<img src="_images/ibmcloud_pi_snap.png" width="850">

- Um den Snapshot zu suchen und die ID des Snapshots herauszufinden nutzen Sie den Befehl ``ibmcloud pi snap ls``

<img src="_images/ibmcloud_snap_ls.png" width="850">

- Um den Snapshot für eine Wiederherstellung zu nutzen müssen Sie die LPAR zuerst herunterfahren
    - Gehen Sie zum herunterfahren über Ihren Workspace unter **Compute** auf **Virtual Server Instances**, wählen Sie Ihre Instanz aus und klicken Sie ganz rechts oben, auf der höhe des Namens, auf das Icon mit den 3 Punkten, klicken Sie dann auf ``OS Shutdown``

<img src="_images/OS_shutdown.png" width="850">

- Sobald die LPAR heruntergefahren ist können Sie den Restore durchführen
- Der Befehl für einen Restore sieht wie folgt aus: ``ibmcloud pi ins snap restore <ID_Instanz> --snapshot <ID_Snapshot>``
- Wenn der Befehl erfolgreich gestartet wurde, sollte der Restore des Snapshots erfolgreich sein

<img src="_images/restore-snapshot.png" width="850">

- Schalten Sie zum Schluss Ihre LPAR wieder aktiv
    - Die LPAR kann genauso gestartet werden wie Sie heruntergefahren wurde, navigieren Sie über das Icon mit den 3 Punkten und wählen Sie ``Start``

<img src="_images/OS_start.png" width="850">

---
#### Volume klonen

 - Um ihr Volume zu klonen müssen Sie zuerst die ID des zu klonenden Volumes herausfinden, am besten machen Sie dies mit dem Befehl ``ibmcloud pi vol ls``
 - Suchen Sie sich das Volume aus, welches Sie klonen möchten und kopieren Sie sich die ID
 - klonen Sie ihr Volume mit dem Befehl ``ibmcloud pi vol cla cr <clone_name> --volumes <ID_volume>``

 <img src="_images/ibmcloud_clone.png" width="850">

 - Wenn Sie jetzt jetzt wieder Ihre Volumes mit ``ibmcloud pi vol ls`` auflisten, müsste das geklonte Volume unter dem von Ihnen vergebenen Namen sichtbar sein

 <img src="_images/ibmcloud_pi_vol_ls.png" width="850">

---
#### Volume clone an neue LPAR hängen

- Erstellen Sie zunächst eine zweite LPAR an die Sie das gekolonte Volme anhängen möchten, befolgen Sie dafür die Schritte aus **01_Workspace_anlegen - Schritt 4: LPAR erstellen**

<img src="_images/LPAR2.png" width="850">

- Finden Sie die ID ihrer neuen Instanz im IBM Cloud Portal oder mit dem Befehl ``ibmcloud pi ins ls`` heraus
- Finden Sie die ID des geklonten Volumes mit ``ibmcloud pi vol ls``heraus
- Attachen Sie das geklonte Volume an Ihre neue LPAR mit dem Befehl: ``ibmcloud pi ins vol attach <ID_Instance> --volumes <ID_cloned_Volume>``

> [!WARNING]
> Warten Sie bis die neue LPAR vollständig hochgefahren ist, ansonsten lässt sich das Volume nicht anhängen

<img src="_images/volume_attached.png" width="850">

- Im IBM Cloud Portal können Sie jetzt unter ``Attached Volumes`` innerhalb Ihrer zweiten Virtual Server Instance das Volume sehen, das Sie zuvor von Ihrer ersten LPAR geklont haben

<img src="_images/volume_attached_Portal.png" width="850">
