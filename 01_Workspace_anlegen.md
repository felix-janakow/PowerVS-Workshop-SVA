# 01_Workspace_anlegen

### Schritt 1 - Login + Navigation zu PowerVS:

- Melden Sie sich mit ihren Login-Daten in ihrem IBM Cloud Account an 
- Suchen Sie im oberen Navigationsbalken nach ``Catalog`` 
- Suchen Sie im Suchfeld des Katalogs nach **PowerVS**
- Wählen Sie **Power Virtual Server aus**

<br/>
<img src="_images/powervs_catalog.png" width="750">

----
### Schritt 2 - PowerVS Workspace erstellen:

- klicken Sie auf das Feld ``Create a Workspace``
- wählen Sie als **Location type** - **IBM data center** 
- wählen Sie als **Location** - **eu-de-1** oder **eu-de-2** (-> Datacenter in Frankfurt, es kann natürlich theoretisch jedes verfügbare Datacenter gewählt werden)

> [!NOTE]
> Eine Auflistung der Standorte an denen Power Virtual Server zur Verfügung stehen finden Sie hier: [Power Virtual Server Regions](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-ibm-cloud-reg)

- gehen Sie anschließend auf ``Continue``
- wählen Sie einen Namen für den Workspace
- als **Resource group** wählen Sie die Ihnen zugeordente Ressourcengruppe 
- **User tags** und **Access management tags** können im Moment ignoeriert werden
- gehen Sie anschließend auf ``Continue``
- der Punkt Monitoring ist optional  (zur optimalen Fehlerbehebung und der Reduzierung von Ausfallzeiten empfohlen) 
- gehen Sie anschließend auf ``Finish``
- setzen Sie den Haken bei ***I agree to the Terms and Conditions*** und wählen Sie zum Schluss ``Create``

<br/>
<img src="_images/create_pvs_workspace.png" width="850">

> [!NOTE]
> Beim reinen anlegen eines Workspaces entstehen keine Kosten

- nachdem der Workspace erstellt ist sollte dieser jetzt in der Ansicht **Workspaces** sichtbar sein
- klicken Sie auf Ihren erstellten Workspace um mit den nächsten Schritten fortfahren zu können

> [!TIP]
> Falls Sie von irgendeinem Punkt in der IBM Cloud aus wieder schnell zu ihrem Workspace navigieren möchten, wählen sie über die Seitenleiste -> ``Resource list`` und suchen Sie unter **Compute** Ihren Workspace
>
> ![Navigation_Ressourcelist](https://github.com/felix-janakow/PowerVS-Workshop-SVA/blob/main/_images/nav_resource-list.png)

----
### Schritt 3:  Subnet und SSH-Key erstellen

#### Subnetz erstellen

- um ein Subnetz zu erstellen navigieren Sie innerhalb ihres Workspaces unter **Networking** auf **Subnets**

<br/>
<img src="_images/navbar_subnets.png" width="230">

- gehen Sie auf der rechten Seite auf das Feld `Create Subnet +`
- bennen Sie ihr Subnet
- vergeben Sie Ihre für diese Übung vorgegebne Subnet-Adresse 
- lassen Sie die restlichen Werte standardmäßg und klicken sie auf ``Teilnetz erstellen``

<br/>
<img src="_images/subnet_create.png" width="270">

#### SHH-Key erstellen

- um einen SSH-Key zu erstellen navigieren Sie innerhalb ihres Workspaces unter **Compute** auf **SSH-keys**

<br/>
<img src="_images/ssh-keys_navbar.png" width="230">

- gehen Sie auf der rechten Seite auf das Feld ``Create SSH-Key``
- vergeben Sie einen Namen für den Key und fügen Sie den öffentlichen Schlüssel ihres SSH-Keys im unteren Feld ein und drücken Sie auf ``Add SSH key``

> [!NOTE]
> Der SSH-Key sollte im vorhinein mit z.b. ``ssh-keygen`` (für Linux und MacOs) erstellt werden
>
> Beispiel: ``ssh-keygen -t rsa -b 4096 -C "test-key"``
>
> Mehr Infos zum generieren und nutzen von SSH-Keys in der offiziellen IBM Cloud Dokumentation -> [generieren und nutzen von SSH-Keys](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-ssh-key)

<br/>
<img src="_images/ssh-key_create.png" width="650">

----
### Schritt 4: LPAR erstellen 

