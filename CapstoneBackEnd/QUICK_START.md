# Quick Start: Deploy to Render

## In 5 Minutes

### 1. **Generate SECRET_KEY**
```bash
python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'
```
Copy the output.

### 2. **Create Render Account**
- Go to [render.com](https://render.com)
- Sign up and connect your GitHub repo

### 3. **Create New Web Service**
- Select "New +" → "Web Service"
- Connect your repository
- Set build command: (leave empty or default)
- Set start command: `gunicorn uninterrup.wsgi`

### 4. **Set Environment Variables**
In Render Dashboard → Environment:
```
SECRET_KEY=[paste the key from step 1]
DEBUG=False
ALLOWED_HOSTS=your-service-name.onrender.com
DB_NAME=your_db_name
DB_USER=your_db_user
DB_PASSWORD=your_secure_password
DB_HOST=your_postgres_host
DB_PORT=5432
CORS_ALLOWED_ORIGINS=https://your-frontend-domain.com
```

### 5. **Add PostgreSQL**
- Click "Add Service" → PostgreSQL
- Render will set DATABASE_URL automatically
- Update your env vars with the credentials

### 6. **Deploy**
- Click "Deploy"
- Wait 2-5 minutes
- Check logs if any errors

### 7. **Create Superuser** (optional)
```bash
render ssh your-service-name
python manage.py createsuperuser
```

---

## Common Issues & Fixes

### Static Files Not Loading
✅ Already configured with WhiteNoise

### Database Connection Error
- Verify DB credentials in environment
- Ensure PostgreSQL is running
- Check DB_HOST is correct

### Migrate Fails
- The Procfile's `release` command handles this
- Check Render logs for details

### 500 Errors
- Check Render logs
- Verify SECRET_KEY is set
- Ensure DEBUG=False

---

## Files You Modified/Created
- ✅ `requirements.txt` - Dependencies
- ✅ `Procfile` - Deployment config
- ✅ `runtime.txt` - Python version
- ✅ `.env.example` - Template env vars
- ✅ `uninterrup/settings.py` - Production settings
- ✅ `DEPLOYMENT_REPORT.md` - Full analysis
- ✅ `DEPLOYMENT.md` - Detailed guide

All set! 🚀
