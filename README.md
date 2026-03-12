# Warehouse Management System (WMS)

A comprehensive Django-based warehouse management system with AI-powered optimization for intelligent stock placement and logistics coordination.

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Docker Setup](#docker-setup)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [Configuration](#configuration)
- [Support](#support)
- [Contributing](#contributing)

## Features

### Core Warehouse Operations
- **Company Management** — Register and manage multiple companies with complete contact information
- **Stock Management** — Track products, inventory levels, and stock movements with batch tracking
- **Service Management** — Manage warehouse services and container operations
- **Courier Integration** — Handle courier options and dispatch tracking

### Advanced Capabilities
- **Role-Based Access Control** — Three user roles (Customer, Operative, Manager) with appropriate permissions
- **Stock History Tracking** — Complete audit trail of all inventory movements (inbound/outbound)
- **Batch & Location Tracking** — Monitor product batches and warehouse locations
- **Dispatch Management** — Track shipments with courier integration and pricing

### AI-Powered Optimization
- **Intelligent Placement** — Deep Q-Network (DQN) agent for optimized warehouse layout
- **Space Optimization** — Maximize storage efficiency using reinforcement learning
- **WarehouseEnv Simulator** — Gym-compatible environment for warehouse operations

## Tech Stack

- **Backend Framework**: Django 5.0.3
- **Database**: MySQL 8.0.11
- **Python**: 3.11
- **ML/AI**: Gymnasium, Stable Baselines3 (DQN)
- **Containerization**: Docker & Docker Compose
- **Image Processing**: OpenCV, Pillow

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- Python 3.11+ (for local development)
- MySQL 8.0+ (or use Docker MySQL container)
- Git

### Installation

#### Local Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd digital-systems-project
   ```

2. **Create a Python virtual environment**
   ```bash
   python3.11 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   ```bash
   cp .env.example .env
   ```
   Edit `.env` with your database credentials:
   ```
   MYSQL_DATABASE=warehouse_db
   MYSQL_USER=warehouse_user
   MYSQL_PASSWORD=your_secure_password
   MYSQL_ROOT_PASSWORD=root_password
   MYSQL_HOST=localhost
   DEBUG=True
   ALLOWED_HOSTS=localhost,127.0.0.1
   ```

5. **Run migrations**
   ```bash
   cd wms
   python manage.py makemigrations
   python manage.py migrate
   ```

6. **Create a superuser**
   ```bash
   python manage.py createsuperuser
   ```

7. **Start the development server**
   ```bash
   python manage.py runserver 0.0.0.0:8000
   ```

   Access the application at `http://localhost:8000`

### Docker Setup

1. **Build and run with Docker Compose**
   ```bash
   docker-compose up -d
   ```

   The system will:
   - Initialize MySQL database
   - Run Django migrations automatically
   - Create a superuser (if configured)
   - Start the web server on port 8000

2. **Access the application**
   - Web UI: `http://localhost:8000`
   - Admin Panel: `http://localhost:8000/admin`
   - Database: `localhost:3306`

3. **Stop the services**
   ```bash
   docker-compose down
   ```

4. **View logs**
   ```bash
   docker-compose logs -f web  # Django logs
   docker-compose logs -f db   # MySQL logs
   ```

## Project Structure

```
├── wms/                          # Django project root
│   ├── CompanyManager/          # Company management app
│   ├── StockManager/            # Inventory & stock tracking
│   ├── ServiceManager/          # Warehouse services
│   ├── CourierManager/          # Courier integration
│   ├── warehouse/               # Core warehouse app & custom user model
│   ├── model/                   # ML/AI models
│   │   ├── envs/               # Gymnasium environment
│   │   │   └── warehouse_env.py # DQN training environment
│   │   └── agents/             # RL agents
│   │       └── dqn_agent_setup.py
│   ├── manage.py
│   └── wms/                     # Django settings
│       ├── settings.py
│       ├── urls.py
│       ├── wsgi.py
│       └── asgi.py
├── docker-compose.yml           # Docker Compose configuration
├── Dockerfile                   # Docker build configuration
├── requirements.txt             # Python dependencies
└── README.md                    # This file
```

## Usage

### Web Interface

1. **Login** with superuser credentials
2. **Dashboard** — Navigate to the main warehouse dashboard
3. **Companies** — Add and manage warehouse companies
4. **Stock** — Input stock, track inventory, dispatch items
5. **Services** — Manage warehouse services
6. **Couriers** — Configure courier options
7. **Admin Panel** — Access Django admin at `/admin/`

### Database Models

#### Core Models
- **CustomUser** — Extended user model with role and company association
- **Company** — Company information with contact details
- **Product** — Product definitions with SKU/Carton types and pricing
- **Stock** — Individual stock items with location and batch tracking
- **StockChange** — Audit log of inventory movements
- **StockDispatch** — Shipment records with courier integration

### API Integration

The system follows Django's REST conventions. Access the admin panel at `/admin/` to manage all models directly.

## Configuration

### Environment Variables

Create a `.env` file in the project root:

```env
# Django
DEBUG=False
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com

# MySQL
MYSQL_DATABASE=warehouse_db
MYSQL_USER=warehouse_user
MYSQL_PASSWORD=secure_password_here
MYSQL_ROOT_PASSWORD=root_secure_password
MYSQL_HOST=db  # Use 'db' for Docker, 'localhost' for local
```

### Django Settings

Key configurations in `wms/wms/settings.py`:
- Database backend: MySQL
- Installed apps: warehouse, StockManager, ServiceManager, CourierManager, CompanyManager
- Media files: Stored in `media/` directory for company documents
- Static files: Managed via Django staticfiles

## Support

### Documentation

- [Django Documentation](https://docs.djangoproject.com/en/5.0/)
- [Gymnasium Documentation](https://gymnasium.farama.org/)
- [Stable Baselines3 Documentation](https://stable-baselines3.readthedocs.io/)

### Troubleshooting

**Database Connection Issues**
```bash
# Check MySQL is running and accessible
docker-compose logs db

# Verify credentials in .env file
```

**Migration Errors**
```bash
# Reset migrations (development only)
python manage.py migrate warehouse zero
python manage.py migrate
```

**Port Already in Use**
```bash
# Change port in docker-compose.yml or Docker Compose command
docker-compose up -d -p 8001:8000
```

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Create a feature branch from `main`
2. Make focused, atomic commits
3. Ensure code follows Django conventions
4. Test your changes locally
5. Submit a pull request with a clear description

For detailed contribution guidelines, see [CONTRIBUTING.md](CONTRIBUTING.md) (if available) or contact the maintainers.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

**Questions?** Open an issue or contact the team on WeChat or email (configured in your Company profile).
