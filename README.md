# LAB7_SM - Analyse Dynamique d'Applications Android avec MobSF

## 📱 Vue d'ensemble
Ce laboratoire documente les résultats d'une analyse dynamique complète de l'application DIVA (Damn Insecure and Vulnerable App) réalisée à l'aide de **MobSF (Mobile Security Framework)**.

---

## 🔍 Procédure complète (rappel)

### 1. Créer l'AVD (sans Play Store)
- **Android Studio** → AVD Manager
- **API 29 ou 30** (x86_64)
- **Nom** : MobSF_DIVA_API_30

### 2. Cloner MobSF
```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
```

### 3. Lancer l'émulateur (script MobSF)
```bash
./scripts/start_avd.sh MobSF_DIVA_API_30
```

### 4. Lancer MobSF via Docker
```bash
docker pull opensecurity/mobile-security-framework-mobsf:latest

docker run -it --rm \
  -p 8000:8000 \
  -e MOBSF_ANALYZER_IDENTIFIER=emulator-5554 \
  opensecurity/mobile-security-framework-mobsf:latest
```

**Accès web** : http://127.0.0.1:8000  
**Identifiants** : mobsf / mobsf

### 5. Télécharger DIVA
- **Source** : payatu/diva-android
- **APK direct** : diva-beta.apk

### 6. Analyser
1. Upload APK → Analyse statique
2. Bouton **Start Dynamic Analysis**
3. Explorer les 13 challenges dans l'émulateur
4. Observer logs + trafic + Frida

---

## ✅ Étapes d'analyse réalisées

### 1. Installation et Configuration
- ✅ Émulateur Android lancé (API 29, x86_64)
- ✅ MobSF configuré et démarré
- ✅ Proxy HTTPS activé pour l'interception réseau
- ✅ Certificat racine MobSF installé sur l'émulateur
- ✅ ADB connecté et reconnu

### 2. Injection de Code Frida

#### 🧠 Éditeur Frida personnalisé

L'éditeur intégré permet d'injecter du code Frida sur mesure :

![Éditeur Frida MobSF](https://github.com/user-attachments/assets/9b8d3fab-b9ea-4d77-87a9-d1a383b507c6)

```javascript
Java.perform(function() {
    console.log("[*] Hooking DIVA...");
    
    // Exemple : hook d'une méthode spécifique
    var targetClass = Java.use("jakhar.aseem.diva.MainActivity");
    targetClass.onCreate.implementation = function(savedInstanceState) {
        console.log("[+] onCreate called !");
        return this.onCreate(savedInstanceState);
    };
});
```

---

## 🧭 Menu principal du Dynamic Analyzer

| Fonction | Description technique | Utilité en analyse |
|----------|------------------------|--------------------|
| **Show Screen** | Mirroring VNC de l'écran | Observation en temps réel |
| **Remove Root CA** | Suppression du certificat racine MobSF | Nettoyage post-analyse |
| **Unset HTTP(S) Proxy** | Désactivation du proxy système | Retour à un réseau normal |
| **TLS/SSL Security Tester** | Tests de validation certifiants | Détection faiblesses SSL/TLS |
| **Exported Activity Tester** | Test des activités exportées | Vérification des vecteurs d'attaque |
| **Activity Tester** | Lancement forcé d'activités | Exploration des écrans internes |
| **Get Dependencies** | Extraction des bibliothèques | Identification des composants tiers |
| **Take a Screenshot** | Capture d'écran distante | Documentation des preuves |
| **Logcat Stream** | Streaming des logs Android | Détection de fuites d'informations |
| **Generate Report** | Export JSON/PDF | Synthèse des vulnérabilités |

---

## 🧪 Résultats des tests dynamiques sur DIVA

![Résultats des tests DIVA](https://github.com/user-attachments/assets/c4d9166e-7751-407f-88e1-0124d29d217d)

| Challenge DIVA | Observation dans MobSF | Niveau de criticité |
|---|---|---|
| **Insecure Logging** | Données sensibles (credentials, tokens) affichées en clair dans Logcat | ⚠️ Élevé |
| **Hardcoding Issues** | Mots de passe et clés API visibles dans le code décompilé | 🔴 Critique |
| **Insecure Data Storage** | Fichiers de préférences et bases de données non chiffrées sur /data/data | ⚠️ Élevé |
| **Access Control** | Intents non validés permettant l'accès à des activités protégées | 🟡 Moyen |
| **Input Validation** | Absence de validation des entrées utilisateur | 🟡 Moyen |
| **Content Provider Leakage** | Provider exporté exposant des données sensibles | 🔴 Critique |

---

## 🛠️ Environnement technique

| Composant | Version / Configuration |
|---|---|
| **Système d'exploitation** | Linux / Windows / macOS |
| **Android Emulator** | API 29 (Android 10), x86_64, sans Google Play |
| **MobSF** | Version latest (Docker) |
| **Frida Server** | Version adaptée à l'API 29 |
| **ADB** | Platform-tools latest |
| **APK testée** | DIVA (Damn Insecure and Vulnerable App) v1.0 |

---

## 🐛 Dépannage rapide

| Problème | Solution |
|---|---|
| **Dynamic Analysis Failed** | Lancer émulateur avant MobSF + vérifier `adb devices` |
| **Docker ne voit pas l'émulateur** | Ajouter `--net=host` (Linux) |
| **Émulateur lent** | Utiliser API 29 x86_64 |
| **Windows** | Utiliser `start_avd.ps1` |
| **adb devices ne montre rien** | `adb kill-server && adb start-server` |
| **Proxy HTTPS inactif** | Problème réseau sous Linux → Ajouter `--net=host` à Docker |
| **Frida ne répond pas** | Télécharger version Frida Server correspondant à l'architecture de l'émulateur |

---

## 🎓 Compétences acquises

| Domaine | Compétences |
|---|---|
| **Environnement** | Configuration d'un AVD rooté sans services Google |
| **Framework** | Maîtrise de MobSF (statique + dynamique) |
| **Instrumentation** | Injection de code Frida, hooking de méthodes Java |
| **Réseau** | Interception et analyse du trafic HTTPS |
| **Analyse** | Détection de vulnérabilités : logging insecure, stockage, intents, hardcoding |
| **Reporting** | Génération de rapports PDF/JSON exploitables |

---

## 📚 Ressources officielles

| Ressource | Lien |
|---|---|
| **MobSF Docs** | [mobsf.github.io](https://mobsf.github.io) |
| **DIVA Android** | [github.com/payatu/diva-android](https://github.com/payatu/diva-android) |
| **OWASP MASTG** | [mas.owasp.org](https://mas.owasp.org) |
| **Frida JavaScript API** | [frida.re/docs/javascript-api/](https://frida.re/docs/javascript-api/) |
| **Android Security Bulletin** | [source.android.com/security](https://source.android.com/security) |

---

## 👤 Auteur

**Soukaina Bachir** – Mobile Security Lab – MLIAEdu 2026
