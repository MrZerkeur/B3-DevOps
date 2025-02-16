# Comment faire fonctionner tout ça - single stage building

- Build l'image
```
docker build . -t *nom souhaité pour l'image*
```

- Run l'image
/!\ Si il existe un .env avec PING_LISTEN_PORT spécifié, alors le "*port conteneur*" doit avoir la même valeur, sinon il doit valoir 3000
```
docker run -p *port hôte*:*port conteneur* *nom souhaité pour l'image*
```

# Test avec trivy

```
axel@Dell-G15:~/Github/B3-DevOps/TP_2$ trivy image devops
2025-02-16T19:26:46+01:00	INFO	[vuln] Vulnerability scanning is enabled
2025-02-16T19:26:46+01:00	INFO	[secret] Secret scanning is enabled
2025-02-16T19:26:46+01:00	INFO	[secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2025-02-16T19:26:46+01:00	INFO	[secret] Please see also https://aquasecurity.github.io/trivy/v0.59/docs/scanner/secret#recommendation for faster secret detection
2025-02-16T19:26:46+01:00	INFO	Detected OS	family="alpine" version="3.21.3"
2025-02-16T19:26:46+01:00	INFO	[alpine] Detecting vulnerabilities...	os_version="3.21" repository="3.21" pkg_num=17
2025-02-16T19:26:46+01:00	INFO	Number of language-specific files	num=1
2025-02-16T19:26:46+01:00	INFO	[node-pkg] Detecting vulnerabilities...

devops (alpine 3.21.3)

Total: 0 (UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 0, CRITICAL: 0)
```
Aucune vulnérabilité trouvée :)

# Quelques explications

J'ai choisi cet ordre de commande pour faire toutes les commandes nécéssaires avant de copier des fichiers, puis copier le packackage.json et .env suivi de l'installation des dépendances pour éviter leur re-installation si le code est modifié mais pas les dépendances.
Enfin le code est copié et transformé en JS, puis exécuté.

# Multi-stage

Je me suis simplement séparé le processus en 2 étapes : la compilation dans le builder et le lancemet dans la seconde étape.

```
docker build -f Dockerfile.multi_stage . -t *nom souhaité pour l'image*
```