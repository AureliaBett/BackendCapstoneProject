# Deployment Checklist for Render

## Pre-Deployment Steps

1. **Generate a new SECRET_KEY**
   - Use Django's secret key generator
   - Do NOT use the example key in settings.py

2. **Update environment variables**
   - Copy `.env.example` to `.env` in Render's environment settings
   - Set secure database credentials
   - Set proper ALLOWED_HOSTS (your Render URL)
   - Set CORS_ALLOWED_ORIGINS (your frontend domain)

3. **Database Setup**
   - Use PostgreSQL add-on from Render
   - Or use external managed PostgreSQL service
   - Ensure DATABASE_URL environment variable is set

4. **Static Files**
   - WhiteNoise is configured to serve static files
   - Run `python manage.py collectstatic --noinput` in Procfile `release` command

5. **SSL/HTTPS**
   - Render automatically provides HTTPS
   - Settings configured to enforce HTTPS in production

6. **Create Render Account and Configure**
   - Create new Web Service on Render
   - Connect your GitHub repository
   - Set Environment Variables in Render dashboard:
     ```
     DB_NAME=your_db_name
     DB_USER=your_db_user
     DB_PASSWORD=your_secure_password
     DB_HOST=your_postgres_host
     DB_PORT=5432
     SECRET_KEY=generate_a_new_secure_key
     DEBUG=False
     ALLOWED_HOSTS=your-app.onrender.com
     CORS_ALLOWED_ORIGINS=https://your-frontend-domain.com
     ```
   - Build command: (leave default)
   - Start command: `gunicorn uninterrup.wsgi`

7. **Run Migrations on Deployment**
   - The Procfile's `release` command will run: `python manage.py migrate`

## Post-Deployment Verification

- [ ] API endpoints respond correctly
- [ ] Authentication tokens are issued
- [ ] Database queries work
- [ ] No DEBUG mode information exposed
- [ ] HTTPS is enforced
- [ ] CORS is working with frontend domain

## Troubleshooting

- Check logs in Render dashboard if deployment fails
- Verify all environment variables are set correctly
- Ensure database connection string is valid
- Check SECRET_KEY is properly set

## Files Created/Modified

- `requirements.txt` - Python dependencies
- `Procfile` - Render deployment configuration
- `runtime.txt` - Python version specification
- `.env.example` - Example environment variables
- `uninterrup/settings.py` - Production-ready settings
