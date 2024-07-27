docker build -t gpt-pro .
docker run -p 3500:3000 -e BASE_URL=https://api.gpt-pro.net -e OPENAI_API_KEY=sk-XIHFJpZ5WGPJooPf6fF0C8C3B64f4e298bE2B6A8C87c2e23 gpt-web
docker tag gpt-pro:latest w1531724247/gpt-pro:latest
docker push w1531724247/gpt-pro:latest

docker run --name gpt-pro-ctn -d --restart always -p 3000:3000 -e SQL_DSN="oneapi_db:Lfc1531724247@tcp(172.31.43.205:3306)/oneapi" -e TZ=Asia/Shanghai -v /home/www/logs/data/one-api:/data w1531724247/gpt-pro
docker update --restart=no gpt-pro-ctn
docker rmi gpt-pro
docker rm -f gpt-pro-ctn


docker update --restart=no airouter-api-ctn

docker run --name gpt-web-ctn -d --restart always -p 3330:3000  -e BASE_URL=https://api.gpt-pro.net -e OPENAI_API_KEY=sk-XIHFJpZ5WGPJooPf6fF0C8C3B64f4e298bE2B6A8C87c2e23 w1531724247/gpt-web
docker update --restart=no gpt-web-ctn
docker rm -f gpt-web-ctn
docker rmi w1531724247/gpt-web


Congratulations! Installed successfully!
========================面板账户登录信息==========================

 外网面板地址: https://34.229.239.74:18753/74fad6eb
 内网面板地址: https://172.31.43.205:18753/74fad6eb
 username: 6bjtghg2
 password: 65d9e747
 