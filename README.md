# ICS Threat Detection System - Backend

FastAPI backend for the Federated Network-Based ICS Threat Detection System.

## Quick Start

```bash
# 1. Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# 4. Run the server
uvicorn app.main:app --reload --port 8000
```

Visit http://localhost:8000/docs for interactive API documentation.

## Full Setup Guide

See [SETUP.md](SETUP.md) for detailed installation and configuration instructions.

## Project Structure

```
backend/
├── app/
│   ├── main.py              # FastAPI application entry point
│   ├── config.py            # Configuration management
│   ├── database.py          # Database connection
│   ├── models/              # SQLAlchemy models
│   ├── schemas/             # Pydantic schemas
│   ├── api/                 # API routes
│   │   ├── alerts.py
│   │   ├── fl_status.py
│   │   ├── predictions.py
│   │   └── demo.py
│   ├── services/            # Business logic
│   │   ├── kafka_consumer.py
│   │   ├── websocket_manager.py
│   │   └── context_buffer.py
│   └── utils/               # Utility functions
├── scripts/                 # Setup and utility scripts
├── tests/                   # Test files
├── alembic/                 # Database migrations
├── requirements.txt         # Python dependencies
├── .env.example            # Environment variables template
└── README.md               # This file
```

## API Endpoints

### Health Check
- `GET /health` - System health status

### Alerts
- `GET /api/alerts` - List all alerts
- `GET /api/alerts/{id}` - Get alert details
- `PUT /api/alerts/{id}/status` - Update alert status

### Federated Learning
- `POST /api/fl/rounds/trigger` - Start new FL round
- `GET /api/fl/rounds` - List FL rounds
- `GET /api/fl/clients` - Get client status

### Attack Predictions
- `GET /api/predictions` - List predictions
- `POST /api/predictions/predict` - Generate prediction

### Demo
- `POST /api/demo/scenarios/{scenario}` - Trigger demo scenario
- `GET /api/demo/status` - Get demo status

### WebSocket
- `WS /ws` - Real-time updates

## Development

### Running Tests
```bash
pytest
pytest --cov=app tests/
```

### Database Migrations
```bash
alembic revision --autogenerate -m "Description"
alembic upgrade head
```

### Code Formatting
```bash
black app/
isort app/
```

## Documentation

- [Setup Guide](SETUP.md) - Detailed installation instructions
- [API Documentation](http://localhost:8000/docs) - Interactive API docs (when running)
- [Architecture](../Idea_and_architecture/docs/network-focused-architecture.md) - System architecture

## Tech Stack

- **FastAPI** - Modern async web framework
- **SQLAlchemy** - Database ORM
- **Pydantic** - Data validation
- **PostgreSQL** - Primary database
- **Redis** - Context buffer storage
- **Kafka** - Event streaming
- **Neo4j** - Graph database for MITRE ATT&CK

## License

[Your License Here]
