# Local

## compilation du code
ng build --configuration production

# Server

## suppression de l'ancien code
rm -rf ~/upload-browser && mkdir -p ~/upload-browser

# Local

## copie du build sur le server
scp -r .\dist\PortFolio\browser\ ubuntu@51.178.39.105:~/upload-browser

# Server

## Déploiement
set -e
sudo mkdir -p /var/www/portfolio/PortFolio
sudo rm -rf /var/www/portfolio/PortFolio/browser
sudo mv ~/upload-browser/browser /var/www/portfolio/PortFolio/
sudo chown -R www-data:www-data /var/www/portfolio
sudo find /var/www/portfolio -type d -exec chmod 755 {} \;
sudo find /var/www/portfolio -type f -exec chmod 644 {} \;
sudo systemctl reload nginx

## Verification : 
curl -I https://myprojectolivier.ovh
