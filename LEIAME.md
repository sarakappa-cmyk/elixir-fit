# Elixir Fit (PWA)

Aplicação que se instala no iPhone e guarda os dados na Google Drive de cada utilizador (pasta privada da app, que nem tu consegues ver).

## 1. Publicar no GitHub Pages
1. Cria um repositório novo no GitHub (ex.: `elixir-fit`).
2. Carrega para lá todos os ficheiros desta pasta (index.html, manifest.webmanifest, sw.js, icon-*.png).
3. Em *Settings → Pages*, escolhe *Deploy from a branch*, branch `main`, pasta `/ (root)`.
4. O endereço fica `https://TEU-UTILIZADOR.github.io/elixir-fit/`.

## 2. Configurar o login Google
1. Vai a https://console.cloud.google.com e cria um projeto.
2. *APIs e serviços → Biblioteca*: ativa a **Google Drive API**.
3. *Ecrã de consentimento OAuth*: tipo **Externo**, preenche o nome da app e o teu email. Em *Âmbitos*, adiciona `.../auth/drive.appdata`.
4. Muda o estado para **Em produção** (em "Teste" só ficam 100 utilizadores e a sessão expira ao fim de 7 dias). Este âmbito não é sensível, por isso normalmente não exige verificação.
5. *Credenciais → Criar credenciais → ID de cliente OAuth → Aplicação Web*.
   Em *Origens JavaScript autorizadas* mete `https://TEU-UTILIZADOR.github.io` (só o domínio, sem `/elixir-fit`).
6. Copia o ID de cliente e cola-o no ficheiro **`config.js`** (substitui o texto entre aspas). Faz commit. Só fazes isto uma vez: nas atualizações seguintes basta substituir o `index.html`.

## 3. Instalar no iPhone
1. Abre o endereço no **Safari**.
2. Toca em Partilhar → **Adicionar ao Ecrã Principal**.
3. Abre a app pelo ícone e toca em **Ligar ao Google Drive**.

## Notas
- Os registos ficam primeiro no telemóvel e a app funciona offline. Sincroniza com a Drive ao tocar em *Sincronizar* e automaticamente após cada registo (enquanto a sessão estiver ativa, cerca de 1 hora).
- Se usares em dois aparelhos, ganha o último que guardou (não há fusão linha a linha).
- Se o login não abrir na app instalada, confirma que os pop-ups não estão bloqueados e testa primeiro no Safari. No iOS, o login Google em apps instaladas tem por vezes comportamentos irregulares.
- Atualizações: normalmente só se substitui o `index.html`. O `config.js` nunca muda.
- Código de barras: usa a câmara (pede permissão no iPhone) e consulta a base Open Food Facts, por isso precisa de internet. Se o produto não existir, preenches à mão e fica guardado.
- Fotos de progresso: ficam só no telemóvel (não vão para a Drive nem para a exportação).

## Vários utilizadores com a Google Drive de cada um (resumo)
1. Cria o projeto no Google Cloud e ativa a Google Drive API.
2. Em Google Auth Platform: Branding (nome Elixir Fit, email de apoio, link da política de privacidade), Audience = Externo e **Publish app** (Em produção), Data Access = só `drive.appdata`.
3. Em Clients cria um ID de cliente do tipo Aplicação Web, com a origem `https://O-TEU-UTILIZADOR.github.io`.
4. Cola o ID em `config.js` e faz commit.
5. Em `privacidade.html` troca `O-TEU-EMAIL` pelo teu email.
Cada pessoa abre o mesmo endereço, instala a app no seu telemóvel e liga a sua conta Google. Os dados ficam na pasta escondida da app, na Drive dela.
