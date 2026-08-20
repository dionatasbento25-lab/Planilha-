# Planilha de Vacinação — pacote para gerar o app Android (.apk)

Este pacote transforma o app em um aplicativo Android de verdade (instalável,
com ícone, funcionando offline) usando **Capacitor** (empacotador) +
**Codemagic** (build na nuvem — não precisa de computador nem Android Studio).

## O que já está pronto aqui
- `www/index.html` — o app completo (mesmo conteúdo do arquivo que você já usa)
- `package.json` — lista as dependências do Capacitor
- `capacitor.config.json` — configuração do app (nome, ícone, pasta web)
- `resources/icon.png` — o ícone (a cabeça de vaca com seringa) que você
  escolheu; o build gera automaticamente todos os tamanhos que o Android
  precisa a partir dele
- `codemagic.yaml` — receita de build: instala tudo, gera o projeto Android,
  gera os ícones e produz um `.apk` pronto para instalar
- O app já está preparado para usar os plugins nativos de **Compartilhar** e
  **Arquivos** do Capacitor quando rodar empacotado — assim exportar PDF e
  backup abrem o menu nativo de salvar/compartilhar do Android.

## Passo a passo (tudo pelo celular, sem computador)

### 1. Criar uma conta no GitHub (se ainda não tiver)
Pelo navegador: github.com → criar conta gratuita.

### 2. Criar um repositório novo
- Botão "New repository"
- Nome: `planilha-vacinacao` (ou o que preferir)
- Deixe **público ou privado**, tanto faz
- Crie vazio (sem README)

### 3. Enviar os arquivos deste pacote para o repositório
No GitHub, use "Add file → Upload files" e envie **todos os arquivos e
pastas deste pacote**, mantendo a estrutura (a pasta `www/` precisa ficar
com o `index.html` dentro dela).

### 4. Criar conta no Codemagic
codemagic.io → criar conta gratuita → conectar com sua conta do GitHub.

### 5. Adicionar o app no Codemagic
- "Add application" → selecione o repositório `planilha-vacinacao`
- Ele deve detectar o `codemagic.yaml` automaticamente (workflow
  "Planilha de Vacinação - Android (APK)")
- Clique em **Start new build**

### 6. Baixar o APK
Quando o build terminar (uns 5–10 minutos), na aba de artefatos vai
aparecer o arquivo `.apk`. Baixe ele direto pelo celular.

### 7. Instalar no celular
- Toque no `.apk` baixado
- Se aparecer aviso de "instalar apps de fontes desconhecidas", autorize
  (é normal para apps fora da Play Store)
- Pronto — o app abre como aplicativo nativo, com ícone próprio, funciona
  offline, e exportar PDF/backup abre o menu de compartilhar do Android

## Sobre o PDF
A geração do PDF (biblioteca jsPDF) ainda depende de internet no momento
de tocar em "Exportar PDF" — isso não muda ao empacotar com Capacitor,
só muda a instalação do app em si. O resto (login, cadastro, lista de
vacinas, backup) funciona 100% offline.

## Se quiser gerar depois um `.apk` "de produção" (assinado, para publicar
na Play Store), isso exige criar uma chave de assinatura e configurar o
Codemagic com ela — um passo a mais que pode ser feito quando for a hora
de publicar de verdade.
