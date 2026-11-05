# Locação de Coordenação de Projeto · Lotes 3 e 5 (SIP · CONSOL)

Painel dos contratos de supervisão do DNIT na Bahia (Lote 3 Itabuna/Eunápolis e Lote 5 Cocos/Jequié).
Arquivo único `index.html`, hospedado no GitHub Pages, com login e dados salvos no Firebase (Authentication + Firestore).

## Arquivos
- `index.html`: o painel inteiro.
- `firebase-config.js`: a configuração do seu projeto Firebase (você preenche).
- `firestore.rules`: regras da fase de montagem, sem login (você cola no Firebase).
- `firestore.rules.com-login`: regras definitivas, só e-mails autorizados (usar quando ligar o login).
- `.nojekyll`: evita que o GitHub Pages processe o site.

> **Fase de montagem:** o painel está configurado com `exigirLogin: false`, sem tela de login. Os passos de Authentication (itens 2 e 3 e o domínio autorizado) ficam para depois. Para ligar o login: ative E-mail/senha, crie os usuários, troque as regras por `firestore.rules.com-login` e mude para `exigirLogin: true` no `firebase-config.js`.

## 1. Criar o projeto Firebase
1. Acesse https://console.firebase.google.com e clique em **Adicionar projeto** (nome sugerido: `sip-locacao-coordenacao`). Pode desativar o Google Analytics.
2. **Authentication** > **Começar** > aba **Sign-in method** > ative **E-mail/senha**.
3. **Authentication** > aba **Usuários** > **Adicionar usuário**: crie o e-mail e a senha de cada pessoa que vai usar.
4. **Firestore Database** > **Criar banco de dados** > modo de produção > região `southamerica-east1` (São Paulo).
5. Firestore > aba **Regras**: apague o conteúdo, cole o texto de `firestore.rules` e clique em **Publicar**. Inclua na lista os e-mails de quem pode acessar.
6. Engrenagem > **Configurações do projeto** > **Seus apps** > ícone **</>** (Web) > registre o app (sem Hosting) e copie o bloco `firebaseConfig`.
7. Cole os valores em `firebase-config.js`.
8. Authentication > **Configurações** > **Domínios autorizados** > **Adicionar domínio**: `SEU-USUARIO.github.io`.

## 2. Publicar no GitHub
1. Crie um repositório novo (por exemplo `locacao-coordenacao`).
2. Envie os 4 arquivos desta pasta para a raiz do repositório (**Add file** > **Upload files**).
3. **Settings** > **Pages** > Source: **Deploy from a branch** > Branch `main`, pasta `/ (root)` > **Save**.
4. Em um ou dois minutos o painel abre em `https://SEU-USUARIO.github.io/locacao-coordenacao/`.

## Como funciona
- Tudo que é editado (estruturas, status, endereços, aluguéis, contatos, prazos, equipe, bases, pendências) é salvo no documento `locacao/estado` do Firestore.
- Quem estiver com o painel aberto recebe as alterações dos outros em tempo real. Se você estiver digitando, a atualização espera você sair do campo.
- A chave `apiKey` do Firebase pode ficar pública no GitHub. A segurança vem do login e das regras do Firestore.
- Limite atual: o painel grava o estado inteiro de uma vez. Se duas pessoas editarem ao mesmo tempo, vale a última gravação.
- Se `firebase-config.js` continuar com "COLE_AQUI", o painel abre em modo local, salvando só no navegador.
