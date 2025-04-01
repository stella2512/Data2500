docker build -t apache443 .

docker run -d -p 8443:443 --name web443 apache443

# Skal vise: hei fra dockerfile 443
curl http://localhost:8443