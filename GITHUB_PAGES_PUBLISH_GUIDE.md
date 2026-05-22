# Guia rapido: publicar um site estatico no GitHub Pages

Use este roteiro quando quiser subir um novo site HTML/CSS/JS para uma URL propria do GitHub Pages.

## 1. Preparar a pasta

Coloque o site em uma pasta com pelo menos:

- `index.html`
- `assets/` se houver imagens, logos, videos ou outros arquivos

## 2. Abrir o PowerShell na pasta

```powershell
cd "CAMINHO_DA_PASTA_DO_SITE"
```

## 3. Iniciar Git e commitar

```powershell
git init
git branch -M main
git add .
git commit -m "Add site"
```

Se o Git pedir nome/e-mail:

```powershell
git config user.name "Rodne"
git config user.email "rodne@example.local"
```

## 4. Logar no GitHub CLI

```powershell
gh auth login --hostname github.com --git-protocol https --web
```

Depois confira:

```powershell
gh auth status
```

Tem que aparecer `Logged in to github.com`.

## 5. Criar repo e subir

Troque `nome-do-site` pelo nome desejado.

```powershell
gh repo create nome-do-site --public --source=. --remote=origin --push
```

## 6. Ativar GitHub Pages

```powershell
$user = gh api user --jq .login
gh api "repos/$user/nome-do-site/pages" -X POST -f "source[branch]=main" -f "source[path]=/"
```

Se disser que Pages ja existe:

```powershell
$user = gh api user --jq .login
gh api "repos/$user/nome-do-site/pages" -X PUT -f "source[branch]=main" -f "source[path]=/"
```

## 7. URL final

```text
https://SEU_USUARIO.github.io/nome-do-site/
```

Para descobrir seu usuario:

```powershell
gh api user --jq .login
```

## 8. Validar

GitHub Pages pode demorar 1 a 3 minutos para sair do 404.

```powershell
Invoke-WebRequest -Uri "https://SEU_USUARIO.github.io/nome-do-site/" -UseBasicParsing
```

## Comando rapido usado neste projeto

```powershell
cd "C:\Users\rodne\Documents\Codex\2026-05-21\https-gemini-google-com-share-3529d423d239"
gh repo create rod-studio-genius --public --source=. --remote=origin --push
gh api "repos/rodneyberthault27-lgtm/rod-studio-genius/pages" -X POST -f "source[branch]=main" -f "source[path]=/"
```

URL publicada:

```text
https://rodneyberthault27-lgtm.github.io/rod-studio-genius/
```
