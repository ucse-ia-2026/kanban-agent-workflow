# Configurar SSH y GitHub CLI

## 1. Generar una clave SSH

Reemplazá el correo por el asociado a tu cuenta de GitHub:

```bash
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_github_ia -C "user@domain.com"
```

## 2. Configurar SSH para GitHub

```bash
cd ~/.ssh/
touch config
```

Editá `~/.ssh/config` y agregá:

```sshconfig
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_github_ia
  IdentitiesOnly yes
```

## 3. Instalar GitHub CLI

```bash
sudo apt update
sudo apt install gh
```

## 4. Iniciar sesión y otorgar permisos

```bash
gh auth login
```

Durante el inicio de sesión, elegí `GitHub.com`, el protocolo `SSH` y cargá la clave pública generada cuando se solicite.

Luego, agregá los permisos necesarios:

```bash
gh auth refresh -h github.com -s "repo workflow write:packages read:org gist notifications user read:project project delete:packages admin:public_key admin:gpg_key"
```

## 5. Verificar la configuración

```bash
ssh -T git@github.com
gh auth status
```
