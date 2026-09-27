# MFA sur Serveur de Messagerie Linux (Postfix + Dovecot)

## Description
Mise en place d'une authentification multi-facteurs (MFA) sur un serveur de messagerie Linux.
L'objectif est de renforcer la sécurité en combinant un mot de passe classique avec un code TOTP généré par Google Authenticator.

## Architecture

| Composant | Rôle |
|-----------|------|
| RedHat 9 (RHEL 9) | Système d'exploitation du serveur mail |
| Postfix | Serveur SMTP — envoi et réception des emails |
| Dovecot | Serveur IMAP/POP3 — consultation des emails |
| Google Authenticator | Génération des codes TOTP (MFA) |
| PAM | Middleware qui connecte Dovecot à Google Authenticator |
| TLS/SSL | Chiffrement des communications (TLSv1.3) |
| VMware 17 Pro | Virtualisation |

## Flux d'Authentification MFA

1. L'utilisateur se connecte via IMAP
2. Dovecot reçoit la demande et la transmet à PAM
3. PAM vérifie le mot de passe via pam_unix.so
4. PAM vérifie le code TOTP via pam_google_authenticator.so
5. Si les deux sont corrects, la connexion est autorisée

## Test MFA

```bash
openssl s_client -connect localhost:993
a LOGIN nihed mail12026CODEOTP
```

Résultat attendu : `a OK Logged in`

## Auteurs
- Nihed Missar
- Emna Brahmi

## ENICarthage — 2026
