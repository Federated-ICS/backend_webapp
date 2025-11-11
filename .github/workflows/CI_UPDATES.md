# CI Pipeline Updates - Phase 2D

## Changes Made

### Added Neo4j Service
- **Image**: `neo4j:5.14`
- **Authentication**: `neo4j/neo4j_password`
- **Ports**: 7474 (HTTP), 7687 (Bolt)
- **Health Check**: Cypher shell connection test
- **Plugins**: APOC (for advanced graph operations)

### New CI Steps

1. **Wait for Neo4j**
   - Polls Neo4j HTTP endpoint until ready
   - Ensures database is fully initialized before tests

2. **Download ICS ATT&CK Data**
   - Downloads latest ICS ATT&CK matrix from MITRE CTI repository
   - Saves to `data/ics-attack.json`
   - Required for MITRE API tests

3. **Import MITRE ATT&CK Data**
   - Runs `scripts/import_mitre_data.py`
   - Imports 95 ICS techniques into Neo4j
   - Marks 1 technique as detected for testing
   - Creates relationships between techniques

### Updated Test Step
- Added Neo4j environment variables:
  - `NEO4J_URI`: bolt://localhost:7687
  - `NEO4J_USER`: neo4j
  - `NEO4J_PASSWORD`: neo4j_password

## Test Coverage

The CI pipeline now tests:
- ✅ PostgreSQL-based APIs (Alerts, FL Status, Predictions)
- ✅ Neo4j-based APIs (MITRE ATT&CK Graph)
- ✅ All 40 backend tests
- ✅ Code coverage reporting
- ✅ Linting (Black, isort, flake8)
- ✅ Type checking (mypy)

## Pipeline Flow

```
1. Start Services (PostgreSQL + Neo4j)
2. Setup Python & Poetry
3. Install Dependencies
4. Wait for PostgreSQL
5. Wait for Neo4j
6. Download ICS ATT&CK Data
7. Import Data to Neo4j
8. Run Database Migrations (PostgreSQL)
9. Run All Tests (40 tests)
10. Upload Coverage Report
```

## Environment Variables

### PostgreSQL
- `DATABASE_URL`: postgresql+asyncpg://ics_user:ics_password@localhost:5432/ics_threat_detection_test

### Neo4j
- `NEO4J_URI`: bolt://localhost:7687
- `NEO4J_USER`: neo4j
- `NEO4J_PASSWORD`: neo4j_password

## Test Execution Time

Estimated CI pipeline duration:
- Service startup: ~30 seconds
- Dependency installation: ~1 minute (cached)
- Data import: ~10 seconds
- Test execution: ~20 seconds
- **Total**: ~2 minutes

## Troubleshooting

### Neo4j Connection Issues
If tests fail with Neo4j connection errors:
1. Check Neo4j health check is passing
2. Verify authentication credentials
3. Ensure ports 7474 and 7687 are accessible
4. Check Neo4j logs in CI output

### Data Import Issues
If MITRE data import fails:
1. Verify curl can access GitHub
2. Check data file is downloaded correctly
3. Ensure Neo4j is ready before import
4. Verify Python script has correct permissions

## Future Enhancements

1. **Cache MITRE Data**
   - Cache downloaded ICS ATT&CK data
   - Reduce download time on subsequent runs

2. **Parallel Testing**
   - Run PostgreSQL and Neo4j tests in parallel
   - Reduce overall CI time

3. **Integration Tests**
   - Add end-to-end API tests
   - Test full attack graph workflows

4. **Performance Tests**
   - Add graph query performance benchmarks
   - Monitor Neo4j query times

---

**Updated**: November 11, 2025
**Status**: ✅ Ready for Production
