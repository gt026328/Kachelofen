# Kachelofen
Yaml code for Home Assistant to manage energy and burned woods of my kachelofen
Based on Kachelofen Temperature measured with an esp32.
Code controls Living room temperature, temperature drop over night while the oven is heating and
suggest next morning amount of burning wood to keep living room warm and cosy

## Installation

### Packages (Entitaeten, Automations, Templates)

Alle Dateien aus `packages/` gehoeren in das Home-Assistant-Verzeichnis `config/packages/`:

```
config/
  configuration.yaml   (enthaelt: homeassistant: packages: !include packages/)
  packages/
    kachelofen.yaml
    kachelofen_automation.yaml
    kachelofen_empfehlung.yaml
    kachelofen_extend.yaml
    kachelofen_fenster_daemmung.yaml
    kachelofen_saison.yaml
```

Nach dem Kopieren: Entwicklerwerkzeuge -> YAML -> "Alle YAML-Konfiguration neu laden".

### Dashboard (Lovelace)

`dashboards/kachelofen_dashboard.yaml` ist **kein Package** und darf NICHT nach
`config/packages/` kopiert werden – auch nicht in einen Unterordner davon. Liegt die
Datei unter `packages/`, bricht HA mit `invalid slug kachelofen-dashboard` ab
(Package-Namen duerfen keinen Bindestrich enthalten).

Einbinden stattdessen als Lovelace-Dashboard im YAML-Modus:

```yaml
# configuration.yaml
lovelace:
  mode: yaml
  dashboards:
    kachelofen-dashboard:   # Url-Pfad MUSS einen Bindestrich enthalten, sonst: "Url path needs to contain a hyphen (-)"
      mode: yaml
      title: Kachelofen
      filename: dashboards/kachelofen_dashboard.yaml
```

Datei nach `config/dashboards/kachelofen_dashboard.yaml` kopieren (nicht nach
`config/packages/`!) und Home Assistant **neu starten** (kein YAML-Reload genuegt
bei Aenderungen an `lovelace.dashboards`). Alternativ im UI ein Dashboard anlegen und
den Inhalt der Datei ueber den YAML-Editor einfuegen.
