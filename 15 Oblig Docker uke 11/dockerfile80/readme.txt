docker build -t apache80 .

docker run -d -p 80:80 --name web80 apache80

# Skal vise: hei fra dockerfile 80
curl http://localhost     