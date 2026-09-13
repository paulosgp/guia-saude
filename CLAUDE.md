# CLAUDE.md — Guia Saúde

A **porta da frente** dos sistemas da Atenção Primária de São Mateus do Sul, em
`https://guiaaps.com.br`. Uma página estática, sem backend, sem login e **sem dado de
paciente** — só o logotipo da Secretaria, o nome e três blocos que levam a cada sistema.

Decidida com o Paulo em 12/09/2026, depois de a conversa do "guarda-chuva" passar por
três desenhos (ver o Artifact *Tela ou app à parte*). O nome é dele: **Guia Saúde**.

## Infraestrutura compartilhada

Vale aqui a regra da pasta raiz — ver [`.claude apps/CLAUDE.md`](../CLAUDE.md). Este app
não toca em Supabase nem em dado sensível, então as regras de RLS e LGPD de lá não o
alcançam; o que se aplica é a de manter este arquivo atualizado sem esperar ser pedido.

## O que é, e o que deliberadamente NÃO é

**É** uma lista de portas. Cada bloco diz o que o sistema é em uma frase, **para quem é**,
e abre o endereço dele em aba nova.

**Não é** um login único. Cada sistema continua pedindo o acesso dele — o AvaliaACS o
dele, o Planifica o dele, e o Guia Clínico não pede nenhum, por decisão antiga do Paulo
("sem cadastro nem chave"). Os rótulos **organizam, não trancam**: a página é pública, e
quem digitar o endereço abre. Quem tranca é cada app.

**Não tem** a seção de documentos da SMS (protocolos, POPs, normas e rotinas). Ela foi
conversada e ele deixou para depois: *"por enquanto não precisa colocar o espaço reservado
para os documentos"*. Quando entrar, entra como uma seção nova, não como um quarto bloco.

## Os três blocos, e por que cada rótulo está escrito assim

| bloco | para quem | endereço |
|---|---|---|
| Planifica Fácil | **Equipe da unidade** | `planifica.guiaaps.com.br` |
| AvaliaACS | Enfermeiros e coordenação | `avalia-acs.web.app` |
| Guia Clínico APS | Enfermeiros e médicos | `guiaclinicoaps.github.io` |

**"Equipe da unidade" e não "ESF Rosas"**: em duas semanas são doze postos, e a porta não
pode envelhecer junto.

## Decisões de construção que não se veem no código

- **As cores saem do logotipo da Secretaria** — o verde do "SAÚDE" e o azul do "SECRETARIA
  DE". Nenhuma paleta inventada: é a identidade que a equipe já reconhece no papel
  timbrado. O arquivo é o mesmo `brasao.png` que as skills de documento usam.
- **O cartão inteiro é clicável**, não só o "Abrir": no celular, isso é a diferença entre
  acertar e errar o toque.
- **O endereço aparece por extenso** embaixo de cada bloco, porque quem divulga precisa
  poder ditá-lo por telefone.
- **No escuro o logotipo ganha uma placa branca.** Ele é colorido sobre fundo transparente;
  sem a placa, o azul do texto some no fundo escuro.
- **Cada link abre em aba nova** (`target="_blank"` + `rel="noopener"`), para a pessoa não
  perder a porta ao fechar o app.
- **Sem biblioteca, sem build.** Um `index.html`, um PNG e o `CNAME`. As fontes vêm do
  Google Fonts com pilha de fallback declarada.

## Hospedagem — GitHub Pages

Repositório `paulosgp/guia-saude`, **público** (o Pages de conta free só serve repositório
público, e a página não tem nada a esconder). O arquivo `CNAME` na raiz é o que diz ao
GitHub qual domínio serve.

**Por que Pages e não Vercel**, já que o Planifica está lá: a CLI da Vercel não está
instalada nem autenticada nesta máquina, então publicar por lá exigiria o Paulo importar o
projeto no painel. Com o Pages, o `gh` (autenticado) faz tudo — sobra para ele só o DNS.
É também o mesmo caminho que o Guia Clínico já usa.

**O DNS fica no Registro.br**, na zona de `guiaaps.com.br` (modo avançado, ligado em
04/09/2026). O subdomínio `planifica` continua apontando para a Vercel — os dois convivem
sem se tocar.

| Tipo | Nome | Dados |
|---|---|---|
| `A` | (vazio, o domínio) | `185.199.108.153` |
| `A` | (vazio) | `185.199.109.153` |
| `A` | (vazio) | `185.199.110.153` |
| `A` | (vazio) | `185.199.111.153` |
| `CNAME` | `www` | `paulosgp.github.io.` |

Depois que o DNS propagar, o certificado HTTPS o próprio GitHub emite (ligar *Enforce
HTTPS* nas configurações do Pages, se não vier ligado sozinho).

## Publicar uma mudança

Editar o `index.html`, commitar e dar push no `main`. O Pages publica sozinho em um ou dois
minutos. Não há build, não há painel, não há segredo em lugar nenhum.
