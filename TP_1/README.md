# Comment lancer cette API

- Cloner le repo

- Ajouter un .env pour y mettre la variable qui définit le port utilisé. Si elle n'est pas défini, alors elle prendra la valeur par défaut de "3000"
```
PING_LISTEN_PORT=8080
```

- Installer les dépendences
```
npm install
```

- Compiler le code
```
npx tsc index.ts
```

- Lancer le code
```
node index.js
```