## How to Run Neo4j

These steps assume Docker Desktop is installed and running.

### 1. Pull the latest changes

```bash
git pull
```

### 2. Navigate to the Neo4j setup directory

```bash
cd infrastructure/neo4j
```

### 3.Start Neo4j (first time setup)

```bash
docker compose up -d
docker start neo4j
```

This will:

- Pull the Neo4j image
- Create the Neo4j container
- Configure ports, volumes, and authentication
- Start the database

### 4.Access Neo4j

- Browser: http://localhost:7474
- Username: neo4j
- Password: neo4j12345

### 5.Verify it’s running

```cypher
RETURN 1 AS ok;
```

If this returns ok = 1, Neo4j is running correctly

### 6. TTL/ Ontology Import (n10s)

Neo4j is configured with the n10s (Neosemantics) plugin to support RDF/Turtle (.ttl) files.
TTL file location
Place .ttl files in

```bash
infrastructure/neo4j/import/
```

They will be accessible inside Neo4j as:

```csharp
file:///import/<filename>.ttl
```

### One-time n10s initialization (per database)

⚠️These commands are executed only once and persist across restarts.

```cypher
CREATE CONSTRAINT n10s_unique_uri IF NOT EXISTS
FOR (r:Resource) REQUIRE r.uri IS UNIQUE;
```

```cypher
CALL n10s.graphconfig.init({
  handleVocabUris: "SHORTEN",
  keepLangTag: true
});
```

### Import a TTL file

Run this for each .ttl file you want to load:

```cypher
CALL n10s.rdf.import.fetch(
  "file:///import/<yourfile>.ttl",
  "Turtle"
);
```

### Verify imported data

```cypher
MATCH (n) RETURN count(n) AS nodes;
MATCH (n)-[r]->(m) RETURN n, r, m LIMIT 25;
```

### 8. Daily usage (after first setup)

Start Neo4j:

```bash
docker start neo4j
```

Stop Neo4j:

```bash
docker stop neo4j
```

Neo4j data and configuration persist as long as the Docker volumes are not deleted.

### Notes

- Neo4j runtime data is stored locally and not comitted to the repository
- TTL files in import/ are not comitted to the repo
- The constraint and n10s configuration do not need to be re-run unless the database is reset
