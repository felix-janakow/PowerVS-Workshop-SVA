# 10a_COS Service und Bucket erstellen

## Vorgehen
1. COS Service erstellen
2. Im COS Service einen Bucket erstellen
3. Zusätzliche Service Credentials mit "Include HMAC Credential" erstellen
4. Service Credentials anzeigen und kopieren für den Image Transfer
5. OS Image Datei / andere Dateien in Bucket hochladen --> Image Transfer in Power Virtual Server Workspace


- Im IBM Cloud Catalog nach „Object Storage“ suchen und diesen Service auswählen:

<img src="_images/COS_Dashboard.png" width="250"/>

- Standard Pricing Plan wählen, nach unten scrollen und ggfs. den Service Name und Resource Group ändern. Rechts Create klicken.
<img src="_images/COS_Service1.png" width="500"/>

- Der Service wird angezeigt, ein Bucket kann ertellt werden. Klick Create bucket:
<img src="_images/COS_Service2.png" width="500"/>

- Gewünschte Bucket Art auswählen und Create klicken - für das Lab z.B. Quickly get started (oder Create a Custom Bucket):
<img src="_images/COS_Create_bucket1.png" width="500"/>
- Ggfs. Name des Buckets ändern, Next klicken, wenn gewünscht, können im nächsten Schritt gleich Dateien hochgeladen werden. Ansonsten auf Next klicken und die Bucket Configuration anschauen. 
<img src="_images/COS_Create_bucket2.png" width="500"/>

<img src="_images/COS_Create_bucket3.png" width="500"/>

In der Bucket Konfiguration finden sich z.B. die Zugriffspfade, diese kopieren, da sie für den Image Transfer benötigt werden:

<img src="_images/COS_Create_bucket1.png" width="500"/>
