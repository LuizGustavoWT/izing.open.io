FROM node:20-bookworm-slim

# Instalar dependências globais
RUN apt-get update \
  && apt-get install -y wget gnupg nano ffmpeg \
  && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
  && apt-get update \
  && apt-get install -y google-chrome-stable fonts-ipafont-gothic fonts-wqy-zenhei fonts-thai-tlwg fonts-kacst fonts-freefont-ttf libxss1 \
  --no-install-recommends \
  && rm -rf /var/lib/apt/lists/*

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true

ENV CHROME_BIN=google-chrome-stable


WORKDIR /app
# Copiar apenas package.json e package-lock.json (se existir)
COPY ./package*.json ./

# Instalar dependências do projeto
RUN npm install

# Copiar os arquivos restantes
COPY . .

# Construir o projeto
RUN npm run build

# Preparar o script de entrada
COPY docker-entrypoint.sh .
RUN chmod +x docker-entrypoint.sh

ENTRYPOINT ["./docker-entrypoint.sh"]
