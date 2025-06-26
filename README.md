# Qdrant Vektor-Datenbank Tutorial

Dieses Projekt demonstriert die grundlegende Nutzung der Qdrant Vektor-Datenbank mit Python. Es zeigt, wie man Collections anlegt, Vektoren einfügt, nach ähnlichen Vektoren sucht, Paging (Scroll), und das Löschen von Punkten/Collections durchführt.

## Inhalt

- Grundlagen zu Vektoren und Vektor-Datenbanken
- Installation benötigter Python-Bibliotheken
- Verbindung zu Qdrant (lokal oder Cloud)
- Collection anlegen und konfigurieren
- Upsert (Einfügen/Aktualisieren) von Vektoren mit Payload
- Ähnlichkeitssuche (`query_points`)
- Pagination mit `scroll`
- Löschen von Punkten und Collections
- Visualisierung von Vektoren und Suchergebnissen

## Voraussetzungen

- Python 3.8+
- Zugang zu einem Qdrant-Server (lokal oder Cloud)
- Eine `.env`-Datei mit deinem Qdrant API-Key und Host (siehe unten)

## Installation

```bash
pip install qdrant-client scikit-learn pandas numpy matplotlib
```

## Nutzung

1. **.env-Datei erstellen:**  
   Kopiere die Datei `.env_sample` zu `.env` und füge deinen Qdrant API-Key sowie den Host hinzu:
   ```env
   QDRANT_API_KEY=dein_api_key
   QDRANT_HOST=dein_qdrant_host
   ```

2. **Notebook öffnen:**  
   Öffne [`tutorial.ipynb`](tutorial.ipynb) in JupyterLab oder VS Code.

3. **Schrittweise ausführen:**  
   Folge den nummerierten Zellen im Notebook. Jede Zelle enthält Erklärungen und Beispielcode. Die Umgebungsvariablen werden automatisch geladen (z.B. mit `python-dotenv`).

4. **Visualisierung:**  
   Am Ende findest du eine 3D-Visualisierung von Vektoren und Suchergebnissen.

## Wichtige Codebeispiele

- **Collection anlegen:**
    ```python
    from qdrant_client.http import models as rest
    collection_name = "my_vectors"
    vector_size = 128
    distance_metric = rest.Distance.COSINE
    client.create_collection(
        collection_name=collection_name,
        vectors_config=rest.VectorParams(
            size=vector_size,
            distance=distance_metric
        )
    )
    ```

- **Vektoren einfügen (Upsert):**
    ```python
    client.upsert(
        collection_name=collection_name,
        points=[...]
    )
    ```

- **Ähnlichkeitssuche:**
    ```python
    response = client.query_points(
        collection_name=collection_name,
        query=query_vector.tolist(),
        limit=3,
        with_payload=True
    )
    ```

- **Pagination (Scroll):**
    ```python
    points_page, next_offset = client.scroll(
        collection_name=collection_name,
        limit=2,
        with_payload=True
    )
    ```

## Lizenz

Dieses Projekt dient ausschließlich zu Lern- und Demonstrationszwecken.
