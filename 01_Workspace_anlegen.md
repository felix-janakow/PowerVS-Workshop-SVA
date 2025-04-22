# 01_Workspace_anlegen

### Schritt 1 - Login + Navigation zu PowerVS:

- Melden Sie sich mit ihren Login-Daten in Ihrem IBM Cloud Account an 
- Suchen Sie im oberen Navigationsbalken nach ``Catalog`` 
- Schen Sie im Suchfeld des Katalogs nach **PowerVS**
- Wählen Sie **Power Virtual Server aus**

<br/>
<img src="_images/powervs_catalog.png" width="750">

----
### Schritt 2 - PowerVS Workspace erstellen:

- Klicken Sie auf das Feld ``Create a Workspace``
- Wählen Sie als **Location type** - **IBM data center** 
- Wählen Sie als **Location** - **eu-de-1** oder **eu-de-2** (-> Datacenter in Frankfurt, es kann natürlich theoretisch jedes verfügbare Datacenter gewählt werden)

> [!NOTE]
> Eine Auflistung der Standorte an denen Power Virtual Server zur Verfügung stehen finden Sie hier: [Power Virtual Server Regions](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-ibm-cloud-reg)

- Gehen Sie anschließend auf ``Continue``
- Wählen Sie einen Namen für den Workspace
- Als **Resource group** wählen Sie die Ihnen zugeordente Ressourcengruppe 
- **User tags** und **Access management tags** können im Moment ignoeriert werden
- Gehen Sie anschließend auf ``Continue``
- Der Punkt Monitoring ist optional (zur optimalen Fehlerbehebung und der Reduzierung von Ausfallzeiten empfohlen)
- Gehen Sie anschließend auf ``Finish``
- Setzen Sie den Haken bei ***I agree to the Terms and Conditions*** und wählen Sie zum Schluss ``Create``

<br/>
<img src="_images/create_pvs_workspace.png" width="850">

> [!NOTE]
> Beim reinen anlegen eines Workspaces entstehen keine Kosten

- Nachdem der Workspace erstellt ist sollte dieser jetzt in der Ansicht **Workspaces** sichtbar sein
- Klicken Sie auf Ihren erstellten Workspace um mit den nächsten Schritten fortfahren zu können

> [!TIP]
> Falls Sie von irgendeinem Punkt in der IBM Cloud aus wieder schnell zu ihrem Workspace navigieren möchten, wählen sie über die Seitenleiste -> ``Resource list`` und suchen Sie unter **Compute** Ihren Workspace
>
> ![Navigation_Ressourcelist](https://github.com/felix-janakow/PowerVS-Workshop-SVA/blob/main/_images/nav_resource-list.png)

> [!NOTE]
> Bitte informieren Sie den Workshop-Leiter, sobald Ihr Power PV Workspace angelegt ist. Er verbindet Ihren Workspace per Transit Gateway mit den weiteren Netzwerken im SVA Workshop Account. Dieser Schritt ist erforderlich, damit Sie später per SSH von Ihrem System auf Ihre Power Instanz zugreifen können.

----
### Schritt 3:  Subnet und SSH-Key erstellen

#### Subnetz erstellen

- Um ein Subnet zu erstellen navigieren Sie innerhalb ihres Workspaces unter **Networking** auf **Subnets**

<br/>
<img src="_images/navbar_subnets.png" width="230">

- Gehen Sie auf der rechten Seite auf das Feld `Create Subnet +`
- Benennen Sie Ihr Subnet
- Vergeben Sie Ihre für diese Übung vorgegebne Subnet-Adresse 
- Lassen Sie die restlichen Werte standardmäßig und klicken sie auf ``Create Subnet``

<br/>
<img src="_images/subnet_create.png" width="270">

#### SSH-Key anlegen

- Um nach dem deployment per SSH auf eine LPAR zugreifen zu können, ist es erforderlich einen SSH Key in Power VS anzulegen, der beim erstellen der LPAR eigebunden wird.  
- Zum Anlegen eines SSH-Keys navigieren Sie innerhalb Ihres Workspaces unter **Compute** auf **SSH-keys**

<br/>
<img src="_images/ssh-keys_navbar.png" width="230">

- Gehen Sie auf der rechten Seite auf das Feld ``Create SSH-Key``
- Vergeben Sie einen Namen für den Key und fügen Sie den **öffentlichen** Schlüssel ihres SSH-Keys im unteren Feld ein und drücken Sie auf ``Add SSH key``

> [!NOTE]
> Der SSH-Key sollte vorher mit z.b. ``ssh-keygen`` (für Linux und MacOs) erstellt werden und nur für diesen Workshop genutzt werden.
> **Beispiel:** ``ssh-keygen -t rsa -b 4096 -C "test-key"``
> Mehr Infos zum generieren und nutzen von SSH-Keys in der offiziellen IBM Cloud Dokumentation -> [generieren und nutzen von SSH-Keys mit Power Virtual Servern](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-ssh-key)

<br/>
<img src="_images/ssh-key_create.png" width="650">

----
### Schritt 4: LPAR erstellen 

- Um die LPAR zu erstellen gehen Sie über **Compute** auf **Virtual Server Instances +**
- Vergeben Sie zuerst einen Namen für Ihre Instanz
- Wählen Sie für **Number of instances** **1** aus
- Wählen Sie unter **SSH key** den Key aus den Sie im vorherigen Schritt erstellt/angelegt haben

> [!NOTE]
> Nehmen Sie sich die Zeit, um sich über das Info-Icon mit den erweiterten Einstellungsmöglichkeiten bei der Provisionierung von Instanzen vertraut zu machen
> weitere Informationen finden Sie in der offiziellen Dokumentation: [Power Virtual Server Dokumentation](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-getting-started)

- Lassen Sie die restlichen Felder auf den Standardeinstellungen und gehen Sie weiter mit ``Continue``
- Wählen Sie ein Betriebssystem aus 
- Wählen Sie ein Image aus 
- Als Storage Tier reicht für diesen Workshop **Tier 3**

> [!NOTE]
> Für mehr Informationen über Storage Tiers lesen Sie in der Dokumentation nach: [Storage Tiers](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers) 

- Wählen Sie für Storage pool ``Auto-select``
- Lassen Sie die restlichen Felder auf den Standardeinstellungen und gehen Sie weiter mit ``Continue``
- Wählen Sie eine Power Maschine aus, welche Sie provisionieren möchten (für die Workshop Zwecke reicht z.b. eine s922)
- Für **Core type** bleiben wir bei der Einstellung **Shared uncapped**
- Für **Cores** wählen wir 0,5 (wird im weiteren Verlauf des Workshops angepasst)
- Für **Virtual Cores** bleiben wir bei der Standardeinstellung 1
- Für **Memory (GiB)** wählen wir 4GB (wird im weiteren Verlauf des Workshops angepasst)
- Gehen Sie weiter mit ``Continue``
- **Storage volumes** lassen wir erst mal aus, diese werden in einem weiteren Teil des Workshops nochmal behandelt
- Gehen Sie weiter mit ``Continue``
- Gehen Sie unter **Network interfaces** auf ``Attach exisitng network + ``
- Wählen Sie ihr zuvor erstelltes Subnet aus, lassen Sie die restlichen Einstellungen wie sie sind und drücken Sie ``Attach``
- Wählen Sie zum Schluss ``Finish``, reviewen Sie den angezeigten Preis, setzen Sie den Haken bei ***I agree to the Terms and conditions*** und wählen Sie ``Create``

<img src="_images/LPAR_provisioning_.png" width="500">
<img src="_images/LPAR_price_.png" width="250">


- Die Provisionierung der Insanz kann jetzt einige Minuten in Anspruch nehmen

----
### Schritt 5: auf die LPAR zugreifen 

- Um auf der Instanz zu arbeiten könen Sie sich nach erfolgreicher Provisonierung zuerst mit dem in der Virtual Private Cloud (VPC) laufenden JumpServer per SSH verbinden ``ssh <Ihr_Username>@<IP_Jump_Server>`` 

> [!NOTE]
> Ihre Username / Passwort Kombination, sowie die IP-Adresse des JumpServers erhalten Sie vom Workshop-Leiter 

- Sobald Sie sich am JumpServer angemeldet haben, können Sie Ihre Power Instanz per ping erreichen
- Die IP Adresse Ihrer Instanz wurde innerhalb des von Ihnen angelegten Subnetztes beim Deployment automatisch vergeben
- Schauen Sie in der Liste der Instanzen oder in den Instanz-Details nach der IP Adresse (siehe [HandsOn Übung 2](02_LPAR_Management.md))
- Damit Sie sich mit Ihrer LPAR per SSH verbinden können, müssen Sie zunächst Ihren **privaten** SSH Key auf den JumpServer übertragen; z.B. mit ``scp ~/.ssh/<workshop-private-ssk-key> <Ihr_Username>@<IP_Jump_Server>:/home/<Ihr Username>/.ssh/<workshop-private-ssk-key>``
- Nun können Sie sich vom JumpServer per SSH mit Ihrer LPAR verbinden ``ssh -s <workshop-private-ssk-key> root@<IP_Ihrer_LPAR>``

> [!NOTE]
> Bitte nutzen Sie, wie oben beschrieben, einen dedizierten SSH-Key für diesen Workshop, keinen Key, den Sie auch an anderer Stelle verwenden!

[Weiter zu Teil 02 LPAR Management](02_LPAR_Management.md)