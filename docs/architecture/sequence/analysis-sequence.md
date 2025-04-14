# Sequenzdiagramm: Ideenanalyse-Prozess

Dieses Sequenzdiagramm zeigt die detaillierte Interaktion zwischen den Systemkomponenten während einer Ideenanalyse.

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant APIGateway
    participant AnalysisService
    participant GPTService
    participant StorageService
    participant DB as Firebase/Supabase
    
    User->>Frontend: Idee eingeben
    Frontend->>Frontend: Validiere Eingabe
    
    Frontend->>APIGateway: POST /api/analyze
    
    APIGateway->>APIGateway: Authenticate & Validate
    
    APIGateway->>AnalysisService: Start Analysis
    
    par Parallel Execution
        AnalysisService->>GPTService: Request Scorecard Analysis
        GPTService->>GPTService: Prepare Prompt
        GPTService->>External: OpenAI API Call
        External-->>GPTService: Scorecard Results
        GPTService-->>AnalysisService: Formatted Scorecard
        
        AnalysisService->>GPTService: Request SWOT Analysis
        GPTService->>GPTService: Prepare Prompt
        GPTService->>External: OpenAI API Call
        External-->>GPTService: SWOT Results
        GPTService-->>AnalysisService: Formatted SWOT
        
        AnalysisService->>GPTService: Request MVP Suggestions
        GPTService->>GPTService: Prepare Prompt
        GPTService->>External: OpenAI API Call
        External-->>GPTService: MVP Results
        GPTService-->>AnalysisService: Formatted MVPs
        
        AnalysisService->>GPTService: Request Risk Analysis
        GPTService->>GPTService: Prepare Prompt
        GPTService->>External: OpenAI API Call
        External-->>GPTService: Risk Results
        GPTService-->>AnalysisService: Formatted Risks
        
        AnalysisService->>GPTService: Request Role Feedback
        GPTService->>GPTService: Prepare Prompt
        GPTService->>External: OpenAI API Call
        External-->>GPTService: Role Feedback
        GPTService-->>AnalysisService: Formatted Feedback
    end
    
    AnalysisService->>AnalysisService: Combine Results
    
    AnalysisService->>StorageService: Save Session
    StorageService->>DB: Store Analysis Data
    DB-->>StorageService: Session ID
    StorageService-->>AnalysisService: Storage Confirmation
    
    AnalysisService-->>APIGateway: Complete Analysis Results
    APIGateway-->>Frontend: Analysis Response
    
    Frontend->>Frontend: Render Results
    Frontend-->>User: Display Analysis Reports
    
    opt Export Results
        User->>Frontend: Request Export (PDF/Notion)
        Frontend->>APIGateway: POST /api/export
        APIGateway->>ExportService: Generate Export
        ExportService->>StorageService: Fetch Session Data
        StorageService->>DB: Query Session
        DB-->>StorageService: Session Data
        StorageService-->>ExportService: Complete Session
        ExportService->>ExportService: Format Export
        ExportService-->>APIGateway: Export URL/Data
        APIGateway-->>Frontend: Export Response
        Frontend-->>User: Download/View Export
    end
```

## Prozessbeschreibung

1. **Initiierung**
   - Der Benutzer gibt seine Geschäftsidee im Frontend ein
   - Das Frontend validiert die Eingabe lokal
   - Die Anfrage wird an den API Gateway gesendet

2. **Analyse-Orchestrierung**
   - Der Analysis Service koordiniert mehrere parallele GPT-Anfragen
   - Jede Analyse (Scorecard, SWOT, MVP, Risiko, Rollen) läuft in einem eigenen Prozess
   - Das GPT Service bereitet spezifische Prompts für jede Analyse vor
   - Die Anfragen werden an die OpenAI API gesendet
   - Die Ergebnisse werden formatiert und strukturiert

3. **Speicherung**
   - Der Analysis Service kombiniert alle Ergebnisse
   - Der Storage Service speichert die Sitzung in der Datenbank
   - Die Session ID wird zurückgegeben

4. **Darstellung**
   - Die Ergebnisse werden an das Frontend übermittelt
   - Das Frontend rendert die verschiedenen Analysekomponenten
   - Der Benutzer sieht die vollständige Analyse

5. **Export (optional)**
   - Der Benutzer kann die Ergebnisse exportieren (PDF, Notion)
   - Der Export Service generiert das entsprechende Format
   - Das Ergebnis wird zum Download oder zur Anzeige bereitgestellt

## Fehlerbehandlung (nicht dargestellt)

- Timeouts bei API-Aufrufen werden mit Retry-Mechanismen behandelt
- Bei GPT-API-Fehlern werden Fallback-Optionen verwendet
- Datenbankfehler werden protokolliert und dem Benutzer mitgeteilt 