# Mini Cheat Sheet IBM Cloud-CLI (für Workshop Inhalte) 


## CLI installieren
    - MacOS: ``curl -fsSL https://clis.cloud.ibm.com/install/osx | sh``
    - Linux: ``curl -fsSL https://clis.cloud.ibm.com/install/linux | sh``
    - Windows: ``iex (New-Object Net.WebClient).DownloadString('https://clis.cloud.ibm.com/install/powershell')``

## Basics
- **CLI updaten:** ``ibmcloud update``
- **CLI Version anzeigen:** ``ibmcloud -v``
- **Login:** ``ibmcloud login``
- **Hilfe:** ``ibmcloud help`` (mit Hilfe arbeiten -> ``ibmcloud pi help`` -> ``ibmcloud pi ins help``)
- **Eigene Ressourcengruppe als Ziel wählen:** ``ibmcloud target -g <ressource_group_name>``
- **Workspace finden und als Ziel wählen:** ``ibmcloud pi ws list`` -> ``ibmcloud pi target <CRN_Workspace>``

## Plugins
- **Alle verfügbaren Plugins auflisten:** ``ibmcloud plugin repo-plugins``
- **PowerVS Plugin installieren:** ``ibmcloud plugin install power-iaas``
- **Alle installierten Plugins auflisten:** ``ibmcloud plugin list``
- **Plugins aktualisieren:** ``ibmcloud plugin update``

## Arbeiten mit Snapshots

- **PowerVS Instanz [+ optionales Volume] snapshotten:** ``ibmcloud pi ins snap cr <ID_Instanz> --name <wählen_sie_einen_Namen> [--volumes <ID_Volume>]``
- **Snapshots auflisten:** ``ibmcloud snap ls``
- **Restore aus Snapshot:** ``ibmcloud pi ins snap restore <ID_Instanz> --snapshot <ID_Snapshot>``

## Klonen von Volumes

**Klon von Volume erstellen:**``ibmcloud pi vol cla cr <clone_name> --volumes <ID_volume>``
**Geklontes Volume auflisten:**``ibmcloud pi vol ls``
**Klon an neue PowerVS Instanz/ LPAR hängen:** ``ibmcloud pi ins vol attach <ID_Instanz> --volumes <ID_cloned_Volume>``

## ID`s leicht herausfinden
- **Virtual Server Instanz/ LPAR`s auflisten** ``ibmcloud pi ins ls`` 
- **Volumes auflisten:** ``ibmcloud pi vol ls``
- **Snapshots auflisten:** ``ibmcloud snap ls``