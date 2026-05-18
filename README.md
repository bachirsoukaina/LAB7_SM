# LAB7_SM - Analyse Dynamique d'Applications Android avec MobSF

## 📱 Vue d'ensemble
Ce laboratoire document les résultats d'une analyse dynamique complète de l'application DIVA (Damn Insecure and Vulnerable App) réalisée à l'aide de **MobSF (Mobile Security Framework)** sur un émulateur Android.

---

## 🔍 Étapes d'analyse réalisées

### 1. Installation et Configuration
- ✅ Émulateur Android lancé (API 29, x86_64)
- ✅ MobSF configuré et démarré
- ✅ Proxy HTTPS activé pour l'interception réseau
- ✅ Certificat racine MobSF installé sur l'émulateur
- ✅ ADB connecté et reconnu

### 2. Injection de Code Frida
J'ai pu écrire et injecter mon propre code Frida directement :

```javascript
Java.perform(function() {
    console.log("[*] Hooking DIVA...");
    // Hooks personnalisés pour l'analyse des fonctions Java
});
```

---

## 🧭 Menu principal du Dynamic Analyzer

| Fonction | Utilité |
|----------|---------|
| **Show Screen** | Mirroring de l'émulateur en temps réel |
| **Remove Root CA** | Supprimer le certificat racine MobSF |
| **Unset HTTP(S) Proxy** | Désactiver l'interception réseau |
| **TLS/SSL Security Tester** | Tester la validation des certificats |
| **Exported Activity Tester** | Tester les activités exposées |
| **Activity Tester** | Lancer des activités internes |
| **Get Dependencies** | Identifier les bibliothèques utilisées |
| **Take a Screenshot** | Capturer l'écran pour documentation |
| **Logcat Stream** | Logs Android en temps réel |
| **Generate Report** | Exporter les résultats en PDF/JSON |

---

## 🧪 Tests dynamiques réalisés avec DIVA

| Challenge DIVA | Ce que j'ai observé dans MobSF |
|----------------|--------------------------------|
| **Insecure Logging** | Logcat affiche des informations sensibles en clair |
| **Hardcoding Issues** | Détection de credentials dans le code |
| **Insecure Data Storage** | Fichiers écrits en clair sur le stockage local |
| **Access Control** | Intents non sécurisés détectés |

---

## 🐛 Dépannage (au cas où)

| Problème | Solution que j'ai appliquée |
|----------|------------------------------|
| **Dynamic Analysis Failed** | Vérifier que l'émulateur est lancé avant MobSF |
| **adb devices ne montre rien** | Redémarrer ADB : `adb kill-server && adb start-server` |
| **Proxy HTTPS ne fonctionne pas** | Vérifier l'option `--net=host` sous Linux |
| **Émulateur trop lent** | Utiliser API 29 x86_64 sans Google Play |

---

## 🎓 Conclusion

Félicitations à moi, **Soukaina Bachir** ! 🎉

J'ai réalisé une analyse dynamique complète conforme aux standards **OWASP MASTG** et **Google Android Security**.

J'ai maintenant la capacité de reproduire ce laboratoire avec d'autres APK vulnérables en suivant la même méthodologie.

### Compétences acquises :
- ✅ Configuration d'un environnement d'analyse dynamique
- ✅ Utilisation avancée de MobSF
- ✅ Injection de code Frida pour le hooking
- ✅ Interception et analyse du trafic réseau
- ✅ Documentation des vulnérabilités découvertes
- ✅ Génération de rapports de sécurité

---

## 📚 Références
- [OWASP MASTG - Dynamic Analysis](https://mas.owasp.org/techniques/android/MASTG-TECH-0033/)
- [MobSF Documentation](https://mobsf.github.io/docs/)
- [Frida Documentation](https://frida.re/)
- [Android Security & Privacy Year in Review](https://security.googleblog.com/)
