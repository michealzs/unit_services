# Systemd Unit Services

Collection of systemd service unit files for deploying Python applications and services on Linux.

## Contents

- `gunicorn_.service` - Gunicorn WSGI HTTP server service template

## Usage

### Installing a Service

1. Copy the service file to systemd directory:
```bash
sudo cp gunicorn_.service /etc/systemd/system/
```

2. Edit the service file to match your application:
```bash
sudo nano /etc/systemd/system/gunicorn_.service
```

Key fields to update:
- `User` - System user to run the service
- `Group` - System group
- `WorkingDirectory` - Path to your application
- `ExecStart` - Path to your application entry point

3. Reload systemd daemon:
```bash
sudo systemctl daemon-reload
```

4. Enable and start the service:
```bash
sudo systemctl enable gunicorn_
sudo systemctl start gunicorn_
```

5. Check service status:
```bash
sudo systemctl status gunicorn_
```

### Service Management Commands

```bash
# Start service
sudo systemctl start gunicorn_

# Stop service
sudo systemctl stop gunicorn_

# Restart service
sudo systemctl restart gunicorn_

# Reload configuration
sudo systemctl reload gunicorn_

# View logs
journalctl -u gunicorn_ -f
```

## Service File Template

```ini
[Unit]
Description=Gunicorn instance to serve application
After=network.target

[Service]
User=your_username
Group=www-data
WorkingDirectory=/path/to/your/app
ExecStart=/path/to/venv/bin/gunicorn --workers 3 --bind unix:app.sock -m 007 wsgi:app

[Install]
WantedBy=multi-user.target
```

## License

MIT
