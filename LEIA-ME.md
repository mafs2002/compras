# Lista de Compras — guia de instalação (≈10 minutos)

Ficheiros desta pasta: `index.html`, `firebase-config.js`, `manifest.webmanifest`, `icon-180.png`, `icon-192.png`, `icon-512.png`.
Precisas de: conta Google (Firebase) e conta GitHub. Tudo gratuito.

## 1. Criar o projeto no Firebase
1. Vai a https://console.firebase.google.com e clica **Criar um projeto** (nome à tua escolha, ex.: `lista-compras`). Pode desativar o Google Analytics.
2. No menu da esquerda: **Criação** (Build) → **Firestore Database** → **Criar base de dados**.
3. Escolhe uma localização na Europa (ex.: `eur3` ou `europe-west`) e inicia em **modo de produção**.

## 2. Colar as regras de acesso
Em Firestore → separador **Regras** (Rules), apaga tudo e cola:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /lists/{id} { allow read, write: if true; }
    match /items/{id} { allow read, write: if true; }
  }
}
```
Clica **Publicar**.

> Nota de segurança: estas regras deixam qualquer pessoa que conheça o teu projeto ler e escrever na lista. Para uso pessoal é aceitável, mas não partilhes o link nem o nome do repositório fora de vocês os dois.

## 3. Obter a configuração
1. No Firebase: ⚙️ **Definições do projeto** → separador **Geral** → secção **As tuas apps** → ícone **`</>`** (Web).
2. Dá um nome (ex.: `compras`), **não** ativar o Firebase Hosting, clica **Registar app**.
3. Copia os valores do objeto `firebaseConfig` que aparece e cola-os no ficheiro **`firebase-config.js`**, no lugar de cada `COLA_AQUI` (mantém as aspas).

## 4. Colocar online no GitHub Pages
1. Em https://github.com cria um **repositório novo** (público; nome simples, ex.: `compras`).
2. **Add file → Upload files** e arrasta **todos os ficheiros desta pasta** (incluindo o `firebase-config.js` já preenchido). Clica **Commit changes**.
3. Vai a **Settings → Pages**. Em *Build and deployment*, escolhe **Deploy from a branch**, branch **main**, pasta **/ (root)** e **Save**.
4. Espera 1–2 minutos. O endereço fica `https://O_TEU_UTILIZADOR.github.io/compras/`.

## 5. Usar no iPhone
1. Abre o endereço no **Safari**.
2. Toca em **Partilhar** → **Adicionar ao ecrã principal**. O ícone do carrinho aparece como uma app.
3. Envia o mesmo endereço à tua namorada e ela faz o mesmo. Não precisa de conta.

## Resolução de problemas
- **"Sem permissão: verifica as regras do Firestore."** → repete o passo 2 e publica as regras.
- **Fica a "A sincronizar…"** → confirma que preencheste o `firebase-config.js` sem deixar nenhum `COLA_AQUI`, e que a base de dados Firestore foi criada.
- **Ícone antigo ou em branco no ecrã principal** → apaga o atalho e volta a adicioná-lo.
- **Alterei um ficheiro e o site não mudou** → espera 1–2 minutos e recarrega a página.

## Notas
- Os itens da versão antiga (dentro do Claude) não são transferidos: a lista começa vazia.
- Funciona com fraca ligação: as alterações guardam-se no telemóvel e sincronizam quando houver rede.
