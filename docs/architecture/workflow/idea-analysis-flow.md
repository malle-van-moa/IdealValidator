# Ideen-Analyse Workflow

Dieser Workflow zeigt den Prozess der Ideen-Eingabe, Analyse und Report-Generierung in der IdeaValidator-Anwendung.

## Workflow-Diagramm

```mermaid
flowchart TD
    A[Benutzer gibt eine Idee ein] --> B{Validierung}
    B -->|Gültig| C[Sendet Anfrage an GPT-Service]
    B -->|Ungültig| A
    
    C --> D[GPT generiert Analysen]
    D --> E1[Scorecard-Analyse]
    D --> E2[SWOT-Analyse]
    D --> E3[MVP Vorschläge]
    D --> E4[Risiko-Analyse]
    D --> E5[Rollen-Feedback]
    
    E1 --> F[Kombiniert Ergebnisse]
    E2 --> F
    E3 --> F
    E4 --> F
    E5 --> F
    
    F --> G[Speichert Session in Datenbank]
    G --> H[Zeigt Analyse-Ergebnisse an]
    
    H --> I{Export wählen}
    I -->|PDF| J1[Generiert PDF-Report]
    I -->|Notion| J2[Exportiert zu Notion]
    I -->|E-Mail| J3[Sendet Report per E-Mail]
    
    J1 --> K[Benutzer erhält vollständigen Report]
    J2 --> K
    J3 --> K
```

## Prozess-Beschreibung

1. **Ideen-Eingabe**: Der Benutzer gibt eine Geschäftsidee oder ein Konzept in das Textfeld ein.
2. **Validierung**: Das System prüft, ob die Eingabe den Mindestanforderungen entspricht.
3. **GPT-Analyse**: Die validierte Eingabe wird an den GPT-Service gesendet.
4. **Analyse-Generierung**: Das System generiert parallel verschiedene Analysetypen:
   - Scorecard-Analyse (10 Kategorien mit Bewertungen 0-10)
   - SWOT-Analyse (Stärken, Schwächen, Chancen, Risiken)
   - MVP-Vorschläge und Validierungs-Roadmap
   - Risiko-Analyse mit Wahrscheinlichkeiten und Gegenmaßnahmen
   - Rollen-basiertes Feedback ("If I were you...")
5. **Ergebnis-Aggregation**: Alle Analysen werden zu einem Gesamtbericht zusammengeführt.
6. **Daten-Speicherung**: Die Session wird in der Datenbank gespeichert.
7. **Ergebnis-Anzeige**: Die Analyse wird dem Benutzer angezeigt.
8. **Export-Optionen**: Der Benutzer kann den Bericht exportieren:
   - Als PDF-Dokument
   - In eine Notion-Vorlage
   - Per E-Mail an sich selbst oder andere

## Technische Interaktionen

- Frontend sendet API-Anfragen an Backend-Services
- Backend kommuniziert mit OpenAI GPT-API
- Ergebnisse werden in Firebase/Supabase gespeichert
- PDF-Generierung erfolgt serverseitig
- Notion-Export nutzt die Notion API
- E-Mail-Versand erfolgt über einen E-Mail-Dienst (SendGrid, etc.) 