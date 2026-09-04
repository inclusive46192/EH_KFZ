# EH_KFZ Werkstattkommunikation

Dieses Glossar beschreibt die fachlichen Begriffe fuer die digitale Annahme und Bearbeitung von Kundenanfragen einer Kfz-Werkstatt.

## Eingang und Bearbeitung

**Anliegen**:
Das fachliche Thema, wegen dem ein Kunde Kontakt aufnimmt, zum Beispiel Statusabfrage, Angebotsanfrage, Terminwunsch oder Notfall.
_Avoid_: Kategorie als alleinige Bezeichnung

**Vorgang**:
Ein nachvollziehbarer Bearbeitungsfall aus einem Kundenkontakt. Ein Vorgang kann einen Anruf, mehrere Nachrichten und eine Rueckrufaufgabe enthalten.
_Avoid_: Ticket, wenn der fachliche Fall gemeint ist

**Rueckrufaufgabe**:
Eine konkrete Aufgabe, einen Kunden zu einem geplanten Zeitpunkt oder Zeitfenster zu kontaktieren.
_Avoid_: Callback als alleiniger Benutzerbegriff

**Prioritaet**:
Die Reihenfolge, in der ein Vorgang bearbeitet werden soll.
_Avoid_: Dringlichkeit als Synonym; Dringlichkeit beschreibt die fachliche Gefahr, nicht nur die Reihenfolge

**Sicherheitskritischer Fall**:
Ein Anliegen mit moeglicher Gefahr fuer Personen, Verkehrssicherheit oder weitere Schaeden am Fahrzeug.
_Avoid_: Notfall fuer jede dringende Anfrage

## Werkstattdaten

**Kunde**:
Eine Person oder Organisation, die mit der Werkstatt kommuniziert.
_Avoid_: User, Account

**Fahrzeug**:
Das Fahrzeug, auf das sich ein Anliegen oder Werkstattauftrag bezieht.
_Avoid_: Objekt

**Kennzeichen**:
Das vom Kunden genannte amtliche Fahrzeugkennzeichen als moeglicher Suchschluessel.
_Avoid_: sichere Identitaet; ein Kennzeichen allein darf eine Auskunft nicht automatisch autorisieren

**Werkstattauftrag**:
Der fachliche Auftrag der Werkstatt fuer ein Fahrzeug, einschliesslich seines Bearbeitungsstatus.
_Avoid_: Ticket

**Auftragsstatus**:
Der von der Werkstatt gepflegte Bearbeitungsstand eines Werkstattauftrags.
_Avoid_: KI-Status

## Kommunikation

**Anruf**:
Ein eingehender oder ausgehender Telefonkontakt mit Zeit, Rufnummer und Bearbeitungsergebnis.

**Transkript**:
Eine maschinell erzeugte Textdarstellung gesprochener Sprache. Sie ist fehlerbehaftet und muss bei unsicheren oder sicherheitskritischen Inhalten bestaetigt werden.
_Avoid_: Protokoll als Synonym

**Kategorisierung**:
Die Zuordnung eines Anliegens zu einem fachlichen Typ.
_Avoid_: automatische Entscheidung; Kategorisierung ersetzt keine menschliche Sicherheitsentscheidung
