{
  "name": "kour-clone",
  "private": true,
  "version": "0.1.0",
  "scripts": {
    "install:all": "npm install && npm install --prefix client && npm install --prefix server",
    "dev": "concurrently -n server,client -c blue,green \"npm run dev --prefix server\" \"npm run dev --prefix client\"",
    "build": "npm run build --prefix client"
  },
  "devDependencies": {
    "concurrently": "^9.1.0"
  }
}
{
  "name": "kour-clone-client",
  "private": true,
  "version": "0.1.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@dimforge/rapier3d-compat": "^0.14.0",
    "socket.io-client": "^4.8.1",
    "three": "^0.170.0"
  },
  "devDependencies": {
    "vite": "^6.0.0"
  }
}
{
  "name": "kour-clone-server",
  "private": true,
  "version": "0.1.0",
  "type": "module",
  "main": "src/index.js",
  "scripts": {
    "dev": "node --watch src/index.js",
    "start": "node src/index.js"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.21.2",
    "socket.io": "^4.8.1"
  }
}
# 1. Create the folders
mkdir -p kour-clone/client/public kour-clone/client/src/{core,world,entities,network,ui} kour-clone/server/src
cd kour-clone

# 2. Save the three package.json files above into:
#    ./package.json   ./client/package.json   ./server/package.json

# 3. Install everything (root + client + server)
npm run install:all

# 4. (Optional) Create empty source files so the structure exists
touch client/index.html client/vite.config.js \
  client/src/main.js client/src/core/{Renderer,Input,Physics}.js \
  client/src/world/Arena.js client/src/entities/{LocalPlayer,RemotePlayer,Weapon}.js \
  client/src/network/Network.js client/src/ui/HUD.js \
  server/src/{index,GameServer,config}.js
printf "node_modules\ndist\n.DS_Store\n" > .gitignore
npm init -y && npm i -D concurrently
cd client && npm init -y && npm i three @dimforge/rapier3d-compat socket.io-client && npm i -D vite && cd ..
cd server && npm init -y && npm i express socket.io cors && cd ..
