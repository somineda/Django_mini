# Django Mini Project

Django 기본 프로젝트 스켈레톤 코드입니다. Docker와 uv를 사용하여 빠르게 개발 환경을 구축할 수 있습니다.

## 요구사항

- Docker
- Docker Compose
- uv (로컬 개발시)

## 시작하기

### 1. 저장소 클론

```bash
git clone <repository-url>
cd Django_mini
```

### 2. Docker 컨테이너 실행

```bash
cd docker
docker-compose up --build
```

### 3. 데이터베이스 마이그레이션

새 터미널에서 실행:
```bash
docker-compose exec web uv run python manage.py migrate
```

### 4. 접속

브라우저에서 http://localhost:8000 접속

## 데이터베이스 정보

PostgreSQL이 Docker 컨테이너로 실행되며 다음 정보로 접속할 수 있습니다:

- **Host**: localhost
- **Port**: 5432
- **Database**: django_mini
- **User**: django
- **Password**: django123

데이터는 Docker volume(`postgres_data`)에 저장되어 컨테이너를 재시작해도 유지됩니다.

## 주요 명령어

### 컨테이너 백그라운드 실행
```bash
docker-compose up -d
```

### 컨테이너 중지
```bash
docker-compose down
```

### Django 명령어 실행
```bash
# 마이그레이션 생성
docker-compose exec web uv run python manage.py makemigrations

# 마이그레이션 적용
docker-compose exec web uv run python manage.py migrate

# 슈퍼유저 생성
docker-compose exec web uv run python manage.py createsuperuser

# Django 쉘 실행
docker-compose exec web uv run python manage.py shell
```

### 로그 확인
```bash
docker-compose logs -f
```

## 프로젝트 구조

```
Django_mini/
├── core/               # Django 프로젝트 설정
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── docker/            # Docker 관련 파일
│   ├── Dockerfile
│   └── docker-compose.yml
├── manage.py
├── pyproject.toml     # 프로젝트 의존성 (uv)
└── uv.lock           # 의존성 잠금 파일
```

## 로컬 개발 (Docker 없이)

로컬에서 개발하려면 PostgreSQL이 설치되어 있어야 합니다.

### 1. PostgreSQL 설치

**macOS (Homebrew):**
```bash
brew install postgresql@16
brew services start postgresql@16
```

**Ubuntu/Debian:**
```bash
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
```

### 2. 데이터베이스 및 사용자 생성

```bash
# PostgreSQL 접속
psql postgres

# SQL 실행
CREATE DATABASE django_mini;
CREATE USER django WITH PASSWORD 'django123';
GRANT ALL PRIVILEGES ON DATABASE django_mini TO django;
\q
```

### 3. uv 설치
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 4. 의존성 설치 및 실행
```bash
# 의존성 설치
uv sync

# 마이그레이션
uv run python manage.py migrate

# 개발 서버 실행
uv run python manage.py runserver
```

## 데이터베이스 마이그레이션

처음 실행시 또는 모델 변경시 마이그레이션을 실행해야 합니다:

```bash
# Docker 사용시
docker-compose exec web uv run python manage.py migrate

# 로컬 개발시
uv run python manage.py migrate
```

## 개발 환경

- Python 3.13
- Django 5.2.8
- Gunicorn 23.0.0
- PostgreSQL 16 (데이터베이스)
- uv (패키지 관리)
# Django_mini
# Django_mini
