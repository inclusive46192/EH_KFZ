# EH_KFZ Heuss

MVP zur Entlastung einer Kfz-Werkstatt von wiederkehrenden Telefonunterbrechungen.

## Projektziel

Anrufe werden strukturiert angenommen, kategorisiert, als Vorgang erfasst und im Werkstatt-Dashboard nach Prioritaet bearbeitet. Sicherheitskritische Anliegen werden sofort an eine verantwortliche Person weitergeleitet; Routineanfragen landen in einer nachvollziehbaren Rueckruf- oder Aufgabenliste.

## Dokumentation

- [MVP-Plan](./docs/MVP-PLAN.md)
- [Ist-Erhebung fuer den Betrieb](./docs/IST-ERHEBUNG.md)
- [Fachliches Glossar](./CONTEXT.md)
- [Architekturentscheidung zum MVP-Schnitt](./docs/adr/0001-kontrollierter-mvp-stufenplan.md)

## Aktueller Stand

Die Werkstattsoftware und der Telefonieanbieter sind noch offen. Deshalb bleibt die erste Version provider- und integrationsfaehig, startet aber mit manueller oder einfacher Import-Pflege, falls keine API verfuegbar ist.