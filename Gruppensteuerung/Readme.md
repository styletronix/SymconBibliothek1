
# Gruppensteuerung
Die Gruppensteuerung ermöglicht das gleichzeitige Schalten mehrerer Endgeräte. Der primäre Zweck ist die Steuerung von Beleuchtung oder Rollos. Allerdings kann die Gruppensteuerung auch universell für andere Zwecke eingesetzt werden. z.B. überall dort, wo der Maximalwert mehrerer Geräte benötigt wird.

Die Gruppensteuerung kann für komplexe Aufgaben kaskadiert werden. Das bedeutet dass eine Gruppe aus mehreren Untergruppen bestehen kann.

## Installation
1.  Fügen Sie SX_SymconExtension zu den Modulen von IP-Symcon hinzu.
2.  Erstellen Sie eine neue Instanz der Gruppensteuerung und speichern Sie die Instanz erst mal ohne weiter Änderung an dieser Stelle
3.  Fügen Sie Links zu schaltbaren variablen in der Kategorie "Geraete" hinzu, welche per Gruppe gesteuert werden sollen.
4.  Öffnen Sie den Instanzeditor und klicken Sie auf "Geräte aktualisieren" damit die Gruppensteuerung die entsprechenden Skripts für die Geräte generiert. Führen Sie diesen Schritt jedes mal aus, wenn Sie Geräte hinzufügen oder entfernen.
5.  Prüfen Sie die Funktion durch verwenden der Taste "An" und "Aus" im Instanzeditor.
6. Fügen Sie gegebenenfalls Bewegungsmelder und Helligkeitssensoren in der entsprechenden Kategorie hinzu und aktualisieren Sie auch dann die Geräte über den Instanzeditor.

Punkt 2 bis 6 wird noch überarbeitet und in künftigen Versionen vereinfacht.

### Profile
Der Status der Geräte kann in Profilen gespeichert werden. Wobei für jedes Profil der einzelstatus der Geräte gespeichert wird. Wird z.b. in einem Profil die Lampe1 auf 50% und die Lampe2 auf 100% gesetzt, wird genau dieser Zustand wiederhergestellt, sobald das Profil wieder aufgerufen wird.

Profile können per Event ausgewählt werden. z.B. ist es möglich für Tags und für Nachts getrennte Profile zu speichern und diese nach Zeit oder einen externen Helligkeitssensor umzuschalten. So geht im Wohnzimmer Tags das Licht mit voller Helligkeit an. Und abends z.b. nur die Stehlampe und das Hauptlicht auf 10% gedimmt.
Ist das Licht bereits durch Bewegungsmelder aktiviert worden, führt ein Wechsel des Profils per Event auch zum sofortigen Umschalten der aktuellen Beleuchtung. Ist das Licht ausgeschaltet führt ein Profilwechsel per Event zu keiner Änderung, bis Bewegung im Raum erkannt wurde.

### Bewegungsmelder
Es werden Bewegungsmelder unterstützt. Sobald Bewegung erkannt wird kann die Gruppe entweder ein-, ausgeschaltet, auf ein bestimmtes Profil gesetzt werden oder den Zustand annehmen in dem sich Geräte zuletzt befanden, als die Bewegung erkannt wurde. Als Bewegungsmelder kann nahezu jedes Gerät verwendet werden, das entweder Abwesend / Anwesend meldet oder nur den Status aktualisiert. So können auch Taster verwendet werden um die Gruppe für eine voreingestellte Zeit einzuschalten. Zusätzlich überwacht die Gruppensteuerung, ob ein Bewegungsmelder auf grund von Störung nicht mehr von Anwesend auf Abwesend meldet. Verbleibt ein Bewegungsmelder also ohne erneute Aktualisierung der Variable auf "Anwesend" wird die Gruppe nach einer einstellbaren Zeit auf "Abwesend" gesetzt.

Vor der Abschaltung der Gruppe kann eine Zeitspanne und ein Level angegeben werden auf das vor der Abschaltung gedimmt werden soll. Wird keine Bewegung mehr erkannt, kann die Gruppe z.b. 20 Sekunden warten, dann die Helligkeit auf 10% stellen, dort nochmals 30 Sekunden warten und dann das Licht ausschalten. So vermeidet man es unerwartet im dunkeln zu stehen.

Bewegungsmelder können über die GUI aktiviert und deaktiviert werden. 

Beispiel:
Ist das Profil für Anwesend "Automatik" und für Abwesend auf "Aus" gestellt, verhält sich die Steuerung wie folgt: Wenn Bewegung erkannt wird (z.B. durch betreten eines Raumes), geschieht erst ein mal nichts. Schaltet man nun das Licht manuell ein, wird dieser Zustand gespeichert. Meldet der Bewegungsmelder nun "Abwesend", wird das Licht im Raum ausgeschaltet. Beim nächsten betreten des Raumes wird das Licht nun in den Zustand gesetzt, wie er zuletzt vor verlassen des Raumes war. Das Licht wird wieder eingeschaltet. Der Status wird dabei für jedes Gerät, welcher der Gruppe zugeordnet ist einzeln gespeichert. Jedes Licht in der Gruppe kann also einen anderen Zustand haben. Dies ist z.b. für Schlafzimmer interessant wo man nachts bei Bewegung nicht unbedingt licht möchte aber dennoch sichergehen will, dass niemand vergisst das licht auszuschalten wenn niemand mehr im Raum ist.

### Steuerung nach Helligkeit
Bewegungsmelder können mit einem Helligkeitssensor kombiniert werden, damit das Licht nur aktiviert wird, wenn dies erforderlich ist. Als Helligkeitssensor kann entweder ein eigener Sensor verwendet werden, oder einen im Bewegungsmelder integrierte Sensor. Wenn der Sensor integriert ist und man für einen Raum (z.b. Treppenhaus) mehrere Bewegungsmelder für eine Gruppe verwendet, kann die Gruppensteuerung so eingestellt werden, dass die Beleuchtung nur aktiviert wird, wenn an dem Bewegungsmelder, welcher die Bewegung erkannt hat, auch die Helligkeit zum einschalten unterschritten wurde. Eine Bewegung im Obergeschoss führt so Tagsüber nicht zu einem einschalten der Gruppe, im dunkeln Keller wird eine Bewegung aber dennoch das Treppenhauslicht aktivieren.

### Alarmbeleuchtung
Die Gruppen verfügen über eine "Alarmbeleuchtung". Wird diese Funktion aktiviert, werden alle Geräte eingeschaltet und können über die Gruppenfunktion nicht mehr abgeschaltet werden. Nach deaktivierung der alarmbeleuchtung kehren alle Geräte in den Zustand vor der aktivierung der Alarmfunktion zurück.

### Manuelle Steuerung
Zur manuellen Steuerung gibt es sowohl einen Schieberegler für Dimmbare Geräte, als auch einen Ein/Aus Schalter für nicht dimmbare Geräte in der Weboberfläche. Werden mehrere Gerätearten in einer Gruppe kombiniert, wird ein dimmen >= 1% automatisch alle nicht dimmbaren Geräte einschalten.

Werden einzelne Geräte nicht über die Gruppe gesteuert, so zeigt die Gruppensteuerung als Status den höchsten Dimm-Wert der Geräte an.

## Verfügbare Befehle
```
SXGRP_UpdateEvents(int $InstanceID);
```
Führt den gleichen Befehl aus wie "Geräte aktualisieren" in der Konfiguration.
Wird in künftigen Versionen entfernt.


```
SXGRP_RefreshPresence(int $InstanceID);
```
Prüft ob sich der Status von Bewegungsmeldern geändert hat. (Nur für interne Verwendung, wird in künftigen Versionen entfernt.)


```
SXGRP_RefreshStatus(int $InstanceID);
```
Prüft ob sich der Status von Geräten geändert hat. (Nur für interne Verwendung, wird in künftigen Versionen entfernt.)


```
SXGRP_RefreshIlluminationLevel(int $InstanceID);
```
Prüft ob sich der Status von Geräten geändert hat. (Nur für interne Verwendung, wird in künftigen Versionen entfernt.)


```
float $minLevel = SXGRP_GetIlluminationLevelMin(int $InstanceID);
```
Liefert den niedrigsten Helligkeitswert aller Helligkeitssensoren.


```
SXGRP_SetState(int $InstanceID, bool $Value);
```
Setzt den Status aller Geräte auf Ein, oder Aus.

```
SXGRP_SetStateFloat(int InstanceID, float $Value);
```
Setzt den Status aller Geräte auf den Wert `$Value`

```
SXGRP_SetStateInteger(int $InstanceID, int $Value);
```
Setzt den Status aller Geräte auf den Wert `$Value`

```
SXGRP_SetAlertState(int $InstanceID, bool $Value);
```
Aktiviert oder deaktiviert die Alarmbeleuchtung.

```
SXGRP_SetManualPresence(int $InstanceID, bool $Value);
```
Setzt die Anwesenheit für eine Gruppe manuell auf "Anwesend" oder "Abwesend". Der  Zustand "Anwesend" hat Vorrang, wenn vorhandene Bewegungsmelder einen anderen Status als die manuelle Einstellung melden.

```
SXGRP_SetPresenceState(int $InstanceID, bool $Value);
```
Nur zur internen Verwendung. Wird in künftigen Versionen entfernt.

```
SXGRP_PresenceTimeoutOff(int $InstanceID);
```
Nur zur internen Verwendung. Wird in künftigen Versionen entfernt.

```
SXGRP_ResetPresenceStateToTemplate(int $InstanceID);
```

```
SXGRP_StoreCurrentAsPresenceStateTemplate(int $InstanceID);
```

```
SXGRP_GetCurrentStateString(int $InstanceID);
```

```
SXGRP_SetCurrentStateString(int $InstanceID);
```

```
SXGRP_CallProfile(int $InstanceID, int $ProfileID);
```

```
SXGRP_UseProfileIDAsPresenceStateTeplate(int $InstanceID, int $ProfileID);
```

```
SXGRP_UseProfileIDAsPresenceStateTeplateAndApplyToCurrentStateIfPresent(int $InstanceID, int $ProfileID);
```

```
SXGRP_StoreProfile(int $InstanceID, int $ProfileID);
```

```
SXGRP_StoreCurrentProfile(int $InstanceID);
```

```
SXGRP_EnablePresenceDetection(int $InstanceID);
```

```
SXGRP_DisablePresenceDetection(int $InstanceID);
```

```
SXGRP_SetProfile(int $InstanceID, int $ProfileID);
```

```
SXGRP_SetProfilePresent(int $InstanceID, int $ProfileID);
```

```
SXGRP_SetProfileAbsent(int $InstanceID, int $ProfileID);
```

```
SXGRP_SetIlluminationLevelMotion(int $InstanceID, int $ProfileID);
```

```
SXGRP_SetIlluminationLevelMotion(int $InstanceID, int $ProfileID);
```
