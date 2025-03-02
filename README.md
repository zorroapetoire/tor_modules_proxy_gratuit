# tor_modules_proxy_gratuit
modules permettant d'utiliser des proxy gratuit
![License](https://img.shields.io/badge/license-MIT-blue.svg)  
**A Python module for anonymous OSINT using Tor and free proxies with ProxyChains**

Ce module permet d'effectuer des recherches OSINT (Open-Source Intelligence) de manière anonyme en s'appuyant sur Tor et des proxys gratuits, intégrés dynamiquement dans ProxyChains. Il est conçu pour contourner les blocages rencontrés par des outils tout en évitant les services payants qui pourraient compromettre l'anonymat.

## Fonctionnalités
- **Rotation des nœuds Tor** : Rafraîchit les circuits Tor pour éviter les nœuds blacklistés.
- **Gestion automatique des proxys** : Récupère et teste des proxys SOCKS5 gratuits depuis des sources publiques.
- **Intégration avec ProxyChains** : Configure dynamiquement `/etc/proxychains4.conf` pour une utilisation transparente avec vos outils OSINT.
- **Anonymat préservé** : Aucun service payant ou traçable n’est utilisé.
- **Modularité** : Peut être intégré comme module dans d'autres scripts Python.

## Prérequis
- **Système d'exploitation** : Kali Linux (ou toute distribution Linux avec Tor et ProxyChains).
- **Dépendances système** :
  - `tor`
  - `proxychains`
- **Dépendances Python** :
  - `requests`
  - `stem`

## Installation

1. **Installer les dépendances système** :
   ```bash
   sudo apt update && sudo apt install tor proxychains -y
   sudo service tor start
   ```

2. **Installer les dépendances Python** :
   ```bash
   pip3 install requests stem
   ```

3. **Cloner le dépôt** :
   ```bash
   git clone https://github.com/[votre-nom-utilisateur]/tor_proxy_module.git
   cd tor_proxy_module
   ```

4. **Vérifier les permissions** :
   Assurez-vous d’avoir les droits d’écriture sur `/etc/proxychains4.conf` (exécutez le script avec `sudo` si nécessaire).

## Utilisation

### En tant que script autonome
Exécutez le script directement pour tester son fonctionnement :
```bash
python3 tor_proxy_module.py
```
Cela :
- Rafraîchit le circuit Tor.
- Récupère et configure jusqu’à 3 proxys gratuits valides.
- Vérifie votre IP publique.
- Exécute un exemple avec TheHarvester.

### En tant que module dans vos scripts
Importez les fonctions dans vos propres projets :
```python
from tor_proxy_module import refresh_tor_identity, update_proxychains, run_osint_tool

# Rafraîchir Tor
refresh_tor_identity()

# Configurer ProxyChains avec 2 proxys valides
update_proxychains(max_proxies=2)

# Exécuter un outil OSINT
run_osint_tool("spiderfoot -t example.com")
```

### Exemple de personnalisation
Pour augmenter le nombre de proxys testés :
```python
update_proxychains(max_proxies=5)
```

## Structure du code
- **`refresh_tor_identity()`** : Change le nœud de sortie Tor.
- **`fetch_free_proxies()`** : Récupère des proxys gratuits depuis des sources publiques.
- **`test_proxy()`** : Vérifie la validité d’un proxy.
- **`update_proxychains()`** : Met à jour la configuration ProxyChains avec Tor et des proxys valides.
- **`check_ip()`** : Affiche votre IP publique actuelle.
- **`run_osint_tool()`** : Lance un outil OSINT via ProxyChains.

## Sources de proxys
Le module utilise des listes publiques gratuites, notamment :
- ProxyScrape
- Proxy-List.download
- Dépôts GitHub (TheSpeedX, jetkai)

Aucune donnée personnelle ou inscription n’est requise.

## Notes sur l’anonymat
- **Tor comme fallback** : Si aucun proxy gratuit n’est valide, le module repose sur Tor.
- **Rotation des User-Agents** : Réduit les risques de détection.
- **Pas de services payants** : Évite tout risque d’identification via des abonnements ou logs.

Pour un anonymat renforcé, configurez des **ponts Tor** dans `/etc/tor/torrc` si les nœuds publics sont bloqués :
```
UseBridges 1
Bridge <IP>:<port> <fingerprint>
```

## Limites
- Les proxys gratuits peuvent être lents ou instables.
- Certains outils OSINT nécessitent des ajustements spécifiques pour fonctionner avec ProxyChains.
- Le test des proxys peut prendre du temps (limité à 30 par défaut).

## Contribution
Les contributions sont les bienvenues ! Si vous avez des idées pour :
- Ajouter des sources de proxys fiables.
- Améliorer la vitesse des tests.
- Contourner des blocages spécifiques.

Ouvrez une **issue** ou soumettez une **pull request**.

## Licence
Ce projet est sous licence [MIT](LICENSE). Vous êtes libre de l’utiliser, le modifier et le distribuer.

## Avertissement
Ce module est destiné à des recherches OSINT légales et éthiques. L’auteur n’est pas responsable d’une utilisation abusive ou illégale.

---

### Instructions pour GitHub
1. Créez un fichier `README.md` avec ce contenu dans le répertoire de votre projet.
2. Ajoutez une licence (par exemple, `LICENSE` avec le texte de la licence MIT) :
   ```plaintext
   MIT License

   Copyright (c) 2025 [Votre nom ou pseudonyme]

   Permission is hereby granted, free of charge, to any person obtaining a copy
   of this software and associated documentation files (the "Software"), to deal
   in the Software without restriction, including without limitation the rights
   to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
   copies of the Software, and to permit persons to whom the Software is
   furnished to do so, subject to the following conditions:

   The above copyright notice and this permission notice shall be included in all
   copies or substantial portions of the Software.

   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
   IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
   FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
   AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
   LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
   OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
   SOFTWARE.
   ```
3. Poussez le tout sur GitHub :
   ```bash
   git init
   git add tor_proxy_module.py README.md LICENSE
   git commit -m "Initial commit with tor_proxy_module and documentation"
   git remote add origin https://github.com/[votre-nom-utilisateur]/tor_proxy_module.git
   git push -u origin main
   ```

Si vous voulez un badge différent, un style plus visuel ou des sections supplémentaires (ex. : FAQ), dites-le-moi !
