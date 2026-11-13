# Gincana: Você ganhou! 🎉

Página para celular onde só os **5 primeiros** registram o nome. Depois disso aparece "Já temos os 5 ganhadores!".
O painel de admin (`/admin`) mostra os nomes em tempo real, permite editar, excluir e zerar, e gera o QR code.

## Arquivos
| Arquivo | Para que serve |
|---|---|
| `index.html` | Página pública (o QR code abre ela) |
| `admin.html` | Painel com senha: ver, editar e excluir ganhadores, baixar o QR code |
| `firebase-config.js` | **Único arquivo que você precisa editar** |
| `firestore.rules` | Regras de segurança (garante no servidor que nunca passa de 5) |

## Configurar o Firebase (uns 5 minutos)
1. Acesse https://console.firebase.google.com e clique em **Criar projeto** (o Analytics pode ficar desligado).
2. **Firestore Database** → *Criar banco de dados* → modo produção → região `southamerica-east1`.
3. Ainda no Firestore, abra a aba **Regras**, cole o conteúdo de `firestore.rules` e clique em **Publicar**.
4. **Authentication** → *Vamos começar* → ative **E-mail/senha**.
   Em **Users** → *Adicionar usuário*: e-mail `admin@gincana.com` e a senha que você quiser.
5. **Configurações do projeto** (engrenagem) → *Seus apps* → ícone **Web `</>`** → registre o app → copie o `firebaseConfig`
   e cole no `firebase-config.js`.

> Se usar outro e-mail de admin, troque nos **dois** lugares: `firebase-config.js` e `firestore.rules`.

## Publicar
Importe o repositório na Vercel (Framework: **Other**, sem build). Pronto:
- Página pública: `https://seu-site.vercel.app`
- Admin: `https://seu-site.vercel.app/admin`

Por fim, abra o admin e clique em **Baixar QR code**: ele já sai com o link certo do site.

## Como funciona o limite
Cada vaga é um documento fixo (`vencedores/1` a `vencedores/5`). A regra só deixa **criar** o documento que ainda não existe,
então mesmo com duas pessoas enviando no mesmo segundo nunca passa de 5. Se o admin excluir alguém, aquela vaga volta a ficar livre.
Cada celular só participa uma vez (fica salvo no navegador do aparelho).
