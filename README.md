# 📺 Tela Digital (TV Corporativa)

Um sistema de Digital Signage (Mural Digital / TV Corporativa) 100% *client-side*, leve, rápido e compatível até mesmo com Smart TVs antigas. 

A aplicação lê uma playlist de mídias (vídeos e imagens) e roda em *loop* infinito, recarregando automaticamente novos conteúdos sem necessidade de intervenção humana.

## ✨ Funcionalidades

- **Compatibilidade Extrema:** O *Player* (`index.html`) foi escrito em **JavaScript ES5 Puro**, garantindo que rode sem travamentos ou telas brancas em navegadores nativos de Smart TVs antigas (WebOS, Tizen, etc).
- **Painel de Controle Integrado:** Uma página administrativa (`config.html`) com interface moderna (Tailwind CSS) para gerenciar a playlist diretamente pelo navegador.
- **Integração Direta com GitHub:** O painel salva as alterações diretamente no arquivo `playlist.json` do seu repositório usando a API do GitHub. Sem necessidade de banco de dados ou backend (PHP/Node).
- **Suporte a Múltiplas Fontes:** Exibe imagens e vídeos hospedados diretamente (Vercel, AWS, etc), além de suporte nativo nativo para **YouTube** (sem anúncios ou vídeos recomendados) e **Google Drive**.
- **Agendamento Inteligente:** Permite definir datas de Início e Fim (`startDate` e `endDate`) para que as mídias entrem e saiam de cartaz sozinhas.
- **Atualização em Tempo Real:** As TVs que estão exibindo o conteúdo consultam o servidor a cada 10 minutos para puxar atualizações feitas pelo painel automaticamente.

---

## 📂 Estrutura do Projeto

- `index.html` → O Reprodutor (Player). É a tela que fica rodando na TV.
- `config.html` → O Painel de Controle (Dashboard) para adicionar, editar e remover mídias.
- `playlist.json` → O banco de dados do sistema, contendo a lista de mídias a serem reproduzidas.

---

## 🚀 Instalação e Hospedagem

Este projeto não necessita de banco de dados ou servidores complexos. Pode ser hospedado gratuitamente no **GitHub Pages** ou **Vercel**.

### Opção Recomendada: Vercel
1. Suba este código para um repositório no seu GitHub.
2. Crie uma conta na Vercel e clique em *Add New Project*.
3. Importe o seu repositório do GitHub.
4. Pronto! A Vercel fornecerá um link (ex: `sua-tela.vercel.app`).

---

## ⚙️ Como usar o Painel de Controle

Para acessar o painel administrativo, basta abrir no navegador:
`https://[SEU-LINK]/config.html`

1. **Senha de Acesso:** A senha padrão para visualizar o painel é **`tvcorporativa`** *(pode ser alterada no código fonte do `config.html`)*.
2. **Configuração do Repositório:** No primeiro acesso, clique em "⚙️ Configurações" e preencha:
   - **Usuário:** Seu usuário do GitHub.
   - **Repositório:** Nome do repositório onde este código está.
   - **Token (PAT):** Um token de acesso gerado no GitHub.

### 🔑 Como gerar o GitHub Token (PAT)
O painel precisa deste token para conseguir editar o arquivo `playlist.json` no seu repositório.
1. Acesse o GitHub e vá em **Settings** > **Developer settings** > **Personal access tokens** > **Tokens (classic)**.
2. Clique em **Generate new token (classic)**.
3. Dê um nome (Ex: "Painel Tela Digital"), coloque validade para *No expiration*.
4. Marque a caixinha **`repo`** (Full control of private repositories).
5. Gere e copie o token (`ghp_...`).

---

## 🎬 Como adicionar Mídias

Ao adicionar uma nova mídia pelo painel, você preencherá a **URL**. O sistema aceita:

- **Vídeos MP4 Diretos:** Cole o link terminado em `.mp4` (Ex: Vercel Blob, Cloudflare R2, servidor próprio). É a opção mais estável.
- **YouTube:** Cole o link comum do YouTube. O sistema automaticamente oculta os controles, remove recomendações externas e força o mute para tocar perfeitamente. Ideal para vídeos pesados.
- **Imagens:** Formatos JPEG, PNG, WEBP via links públicos diretos.
- **Google Drive:** Suportado para vídeos leves ou imagens. *(Aviso: Para vídeos muito pesados, o próprio Google pode bloquear a execução automática forçando uma tela de verificação de vírus).*

### Outros Campos:
- **Duração:** Tempo que o item ficará na tela (Padrão: `00:00:30` - 30 segundos).
- **Ativo:** Se a mídia está ligada (`true`) ou pausada/arquivada temporariamente (`false`).
- **Data Início / Fim (Opcionais):** Formato `DD/MM/AAAA`. Determina quando a mídia entra ou sai automaticamente. Se deixados em branco, o item tocará sempre.

---

## 🔧 Tecnologias Utilizadas

- HTML5, CSS3, JavaScript (ES5 para player, ES6+ para Painel).
- Tailwind CSS via CDN.
- GitHub REST API (`https://api.github.com/repos/...`).