# Crear certificado SSL desde cero


### 1. Instala Nginx

```bash
sudo apt-get update
sudo apt-get install nginx
```

### 2. Configura Nginx para que actúe como proxy inverso

```bash
sudo nano /etc/nginx/sites-available/YOUR_SERVER_NAME
```

Dentro del archivo copiar lo siguiente (cambiando YOUR_DOMAIN y YOUR_PORT):

```nginx
server {
    listen 80;
    server_name YOUR_DOMAIN;

    location / {
        proxy_pass http://localhost:YOUR_PORT;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### 3. Habilita el sitio configurado

```bash
sudo ln -s /etc/nginx/sites-available/YOUR_SERVER_NAME /etc/nginx/sites-enabled
```

### 4. Reinicia Nginx para que los cambios surtan efecto

```bash
sudo systemctl restart nginx
```

### 5. Instala Certbot

```bash
sudo apt-get install certbot python3-certbot-nginx
```

### 6. Configura SSL con Certbot

```bash
sudo certbot --nginx -d YOUR_DOMAIN
```

### 7. Renovación Automática del Certificado
```bash
sudo certbot renew --dry-run
```

## License

[MIT](https://choosealicense.com/licenses/mit/)
