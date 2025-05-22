FROM node:18

WORKDIR /app

# Copier les fichiers nécessaires
COPY package*.json ./
RUN npm install

# Installer ngrok globalement pour éviter l’erreur
RUN npm install -g @expo/ngrok

# Copier le reste du projet
COPY . .

# Expo utilise les ports 19000 (app), 19001 (web), 19002 (devtools)
EXPOSE 19000 19001 19002

# Lancer Expo sans interaction
CMD ["npx", "expo", "start", "--tunnel", "--non-interactive"]
