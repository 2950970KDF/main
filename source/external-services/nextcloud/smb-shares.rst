==================================
Zugriff auf die Home-Verzeichnisse
==================================

.. sectionauthor:: `@cweikl <https://ask.linuxmuster.net/u/cweikl>`_ , `@rettich <https://ask.linuxmuster.net/u/rettich>`_

Die Benutzer können sich jetzt an der Nextcloud anmelden. Was noch fehlt ist, dass sie auf Ihre Daten auf dem Schulserver zugreifen können. Was du nicht möchtest ist, dass die Benutzer Daten auf der Nextcloud ablegen, auf die sie von einem Rechner in der Schule keinen direkten Zugriff haben.

Aktivierung der App External storage support
============================================

Als erstes musst du die App ``External storage support`` aktivieren.

.. image:: media/SMB01.png
   :alt: +Apps
   :align: center
   
Gehe dazu auf A -> + Apps. Auf der Seite ganz unten findest du die deaktivierten Apps. Aktiviere ``External storage support``.


   
Einbindung der Home- und Tauschverzeichnisse
============================================
   
Sollte der Nextloud-Server extern betrieben werden, so muss die OPNsense®-Firewall so konfiguriert werden, dass Anfragen 
über die SMB-Ports 139 und 445 an den Server weitergeleitet werden. 

In der Konfigurationsoberfläche ist unter ``Firewall -> NAT -> Portweiterleitung``
eine entsprechende Regel anzulegen.   
   
.. image:: media/SMB02.png
   :alt: Externer Speicher
   :align: center

In den Einstellungen von ``Externer Speicher`` kannst du jetzt, wie oben im Bild zu sehen ist, die Tauschverzeichnisse und das Home-Verzeichnis ``/`` der Benutzer einbinden.

 .. warning::
    Das Share ``/`` ist das Wurzelverzeichnis der Benutzer. Wenn sich ein Benutzer nicht am Schulserver anmelden kann, kann er sich auch nicht an der Nextcloud anmelden. Und das trifft für den Admin der Nextcloud zu!!!
    Für den Share ``/`` müssen also die Gruppen angegeben werden, die Zugriff auf ein Home-Verzeichnis haben sollen. Sonst kann sich der Admin an der Nextcloud nicht mehr anmelden!!!

.. image:: media/SMB03.png
   :alt: Anmeldedaten
   :align: center

Achte darauf, dass du ``Anmeldedaten in Datenbank speichern`` wählst.

.. image:: media/SMB04.png
   :alt: Vorschau aktivieren
   :align: center
   
Ob du die Vorschau aktivierst oder nicht hängt vom Standort der Nextcloud ab. Ist die Nextcloud nicht in der Schule gehostet und ist deine Internet-Verbindung eher langsam, so ist es besser, wenn du den Haken bei ``Vorschau aktivieren`` nicht setzt.

Am Anfang scheint der Server noch langsam zu sein. Das liegt daran, dass die External Storage App einen Datei-Index aufbaut. Bei mir an der Schule hat das ca. 12 Stunden gedauert. Danach läuft die Nextcloud flott.


