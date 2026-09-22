# CLAUDE.md — Guia Saúde

A **porta da frente** dos sistemas da Atenção Primária de São Mateus do Sul, em
`https://saudesaomateusdosul.com.br` (era `guiaaps.com.br` até 14/09/2026 — ver "A troca de
endereço", abaixo). Uma página estática, sem backend, sem login e **sem dado de
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

**Tem, desde 13/09/2026, a seção "Documentos"** — hoje com dois cartões (o segundo está
logo abaixo). Nasceu com um só: o **Protocolos Institucionais**
(`documentos.guiaaps.com.br`), a busca nos protocolos, POPs, normas e rotinas, regimentos e
planejamentos assinados. Ela entrou como **seção nova** (um `<h2>` e uma
grade própria), e não como quinto bloco em "Sistemas", porque foi assim que ele decidiu quando
deixou o espaço para depois: documento não é sistema onde a equipe trabalha, é o que a equipe
consulta. O ícone `logo-documentos.svg` é nosso (folha com carimbo e lupa, nas cores do
logotipo) — o app nasceu no mesmo dia e não tinha marca; o mesmo arquivo é o favicon dele
(`Documentos Institucionais/src/app/icon.svg` — a pasta local guardou o
nome antigo). Rótulo "Toda a equipe": o app não pede senha, só o posto da pessoa. O cartão foi
posto no ar antes do app existir, por pedido dele, e apontou para lugar nenhum até o DNS e a
Vercel serem configurados — o que saiu no mesmo 13/09/2026.

**O cartão dizia "Documentos Institucionais" até 21/09/2026**, quando o Paulo renomeou o app
para **Protocolos Institucionais**. Mudou só o nome impresso no cartão: o `<h2>` da seção
continua "Documentos" — o Paulo chegou a pedir "Protocolos" ali também, em 22/09/2026, e
recuou ao ver que a seção já tinha ganhado o cartão da Central de Documentos: o `<h2>` é o nome
da PRATELEIRA, e ela hoje guarda dois sistemas diferentes, um só dos quais é de protocolo (o
motivo anterior continua valendo por dentro: nem o acervo do app é só protocolo — tem POPs,
normas, regimentos e planejamentos). O endereço `documentos.guiaaps.com.br` também ficou como
estava — nome de app e nome de infraestrutura são coisas separadas, e o porquê de cada peça que
não foi renomeada está no `CLAUDE.md` daquele app, seção "O nome".

**Desde 21/09/2026 a seção "Documentos" tem um segundo cartão: a Central de Documentos**
(`central.saudesaomateusdosul.com.br`; apontou para o provisório `paulosgp.github.io/central-documentos`
por algumas horas em 22/09/2026, até o CNAME publicar, como foi com o Encaminha). É o acervo
de modelos e formulários da SMS para **baixar** (memorando, ponto manual, férias…) — coisa que a
equipe consulta, não sistema onde trabalha, e por isso entrou em "Documentos", ao lado dos
Protocolos, e não em "Sistemas". Ícone `logo-central.svg` (pasta com seta para baixo), o mesmo
arquivo que é o favicon do app. Com dois cartões de cada lado, o `.duplas` passou de 1/3 + 2/3
para **metade a metade**. Desenho em `../CentralDocumentos/CLAUDE.md`.

**E a seção "Prefeitura", desde 13/09/2026**, com os dois sistemas da Prefeitura (Oxy/Elotech):
**Assinatura Digital** e **Processo Digital**. Entraram como seção própria, e não em "Sistemas",
porque não são da Saúde nem do cuidado — são a papelada administrativa do município, que só parte
da equipe usa. A cor diz o mesmo: os ícones dos dois têm fundo **azul**, enquanto os nossos têm
fundo verde.

### Os links são os endereços-BASE, não os que o Paulo mandou

Ele mandou os dois endereços copiados do navegador, e os dois eram **URLs de sessão de login**
(`openid.oxy.elotech.com.br/...?execution=...&tab_id=...&state=...&nonce=...&code_challenge=...`).
Aqueles parâmetros são de uso único: colados na página, funcionariam hoje para ele e dariam erro de
sessão inválida para qualquer outra pessoa, em qualquer outro dia. O que ficou no cartão é a porta
estável de cada sistema, conferida respondendo 200:

- `https://saomateusdosul.oxy.elotech.com.br/assinatura-digital/`
- `https://saomateusdosul.oxy.elotech.com.br/processo-digital/`

É o próprio sistema que manda a pessoa ao login do Oxy e a traz de volta. O endereço do
Processo Digital que ele mandou tinha ainda o **id do setor e o exercício de 2026** embutidos
(`.../e53a...m8a2026/inbox?setor=d6fdcea1...`) — a caixa de entrada DELE. Fixar isso no cartão
mandaria todo mundo à caixa de um setor só, e quebraria na virada do ano.

## Os três blocos, e por que cada rótulo está escrito assim

| bloco | para quem | endereço |
|---|---|---|
| Planifica Fácil | **Equipe da unidade** | `planifica.guiaaps.com.br` |
| SIGSS | Toda a equipe | `c3102prd.cloudmv.com.br` |
| AvaliaACS | Enfermeiros e coordenação | `avalia-acs.web.app` |
| Guia Clínico APS | Enfermeiros e médicos | `guiaclinicoaps.github.io` |
| Assinatura Digital | Quem assina documento | `saomateusdosul.oxy.elotech.com.br` |
| Processo Digital | Coordenação e chefias | `saomateusdosul.oxy.elotech.com.br` |

**O SIGSS entrou em 13/09/2026, a pedido dele.** É o único bloco que não é sistema nosso — é o
sistema da Secretaria (cloudMV), onde a equipe passa o dia e onde as agentes registram as visitas.
Fica em segundo lugar, logo depois do Planifica: por frequência de uso ele seria o primeiro, mas a
porta é do Guia Saúde e abre pelo que é dele. O endereço não é segredo (está no histórico do
navegador de todo mundo do posto), e o link leva direto à tela de login.

**"Equipe da unidade" e não "ESF Rosas"**: em duas semanas são doze postos, e a porta não
pode envelhecer junto.

## Decisões de construção que não se veem no código

- **As cores saem do logotipo da Secretaria** — o verde do "SAÚDE" e o azul do "SECRETARIA
  DE". Nenhuma paleta inventada: é a identidade que a equipe já reconhece no papel
  timbrado. O arquivo é o mesmo `brasao.png` que as skills de documento usam.
- **São DUAS marcas no alto, desde 13/09/2026** (pedido do Paulo): a da Prefeitura
  (`logo-prefeitura.png`, o `img/logo_mobile.png` do site oficial `saomateusdosul.pr.gov.br`) e a
  da Secretaria de Saúde, nessa ordem — a mesma do papel timbrado, o guarda-chuva antes de quem é
  a porta. **Casadas pela ALTURA e não pela largura**: as proporções são diferentes (345×100 e
  673×202), e o que precisa bater de tamanho é o brasão dentro de cada uma. Se fossem casadas pela
  largura, o brasão da Prefeitura sairia visivelmente menor que o da Saúde ao lado. As duas
  dividem a mesma placa branca no modo escuro.
- **Cada bloco mostra o logotipo do próprio sistema** (pedido do Paulo em 13/09/2026, "coloque a
  logo de cada app"). Os três nossos saíram da pasta de cada um — `logo-planifica.png` (o ícone do
  PWA, `Planifica Facil/public/icons/icon-192.png`), `logo-avaliaacs.svg` (`AvaliaACS/public/icon.svg`)
  e `logo-guiaclinico.png` (`GuiaClinico/_logo/icone_96.png`).
- **O do SIGSS veio DELE, e é por isso que ele está aqui.** Na primeira versão o SIGSS ficou com um
  quadrado verde desenhado, porque é sistema de terceiro (cloudMV) e baixar a marca de outra empresa
  para hospedar na nossa página não é coisa que se faça sem perguntar. Ele viu a página e mandou o
  arquivo ("use este para o siggs") — então a autorização é dele, e o desenho saiu junto com a classe
  `.tile`, que existia só para aquele caso.
- **A arte do SIGSS chegou como foto retangular (492×416) e foi RECORTADA**, não esticada: um
  quadrado de 320 px centrado na marca (que ocupa x 153–415, y 76–333), reduzido a 128 px — três
  vezes os 34 px da tela, que cobre qualquer densidade de celular. O recorte foi feito com
  `System.Drawing` pelo PowerShell (não há biblioteca de imagem instalada nesta máquina) e o fundo
  quase-preto foi **achatado na cor exata** antes de salvar: o ruído de JPEG no fundo fazia o PNG
  sair com 82 KB: achatado, são 13 KB. Se a arte precisar ser refeita, os números do recorte estão
  aqui.
- **A Assinatura e o Processo Digital usam a MESMA marca, o "oxy" oficial** (`logo-oxy.svg`), e
  isso não é descuido: os dois são módulos da mesma plataforma da Elotech e não têm marca própria.
  Procuramos: o bundle do Oxy traz um ícone por módulo (`administracao-ouvidoria.png`,
  `arrecadacao-cemiterio.png` e dezenas de outros), e **nenhum** para esses dois. O que cada um
  declara como ícone é a marca da plataforma — o Processo Digital usa o "oxy" inteiro, e a
  Assinatura Digital um recorte da letra "y" que, nos 34 px do cartão, vira um borrão verde sem
  significado. Então os dois levam o `oxy-logo.svg` (vetor, tirado de
  `assinatura-digital/img/modules/oxy-logo.svg`), e quem separa um do outro é o nome ao lado.
  Na primeira versão esses dois cartões tiveram ícones DESENHADOS aqui, porque baixar a marca de
  uma empresa de fora sem perguntar não é coisa que se faça — foi o Paulo quem pediu as oficiais
  em 13/09/2026, e a autorização é dele (mesma história do ícone do SIGSS).
- **O "oxy" é a única marca DEITADA da página** (2,2:1) e por isso tem regra própria,
  `.topo img.marca-oxy`: 64 px de largura em vez de 34, e sem arredondamento. Espremido no quadrado
  dos outros ele sairia com 15 px de altura e ninguém leria.
- **Os logotipos são CÓPIAS, não links para a pasta do outro app.** Cada app é um repositório
  próprio, e o Pages só serve o que está neste. Trocar a arte de um deles não atualiza esta página
  sozinho — é copiar o arquivo de novo.
- **O arredondamento de 8 px é nosso, não das artes.** As quatro chegam em quadrado de canto vivo;
  ao lado de cartões arredondados isso fica duro. É a única coisa que o CSS faz com elas.
- **O ícone da aba é o BRASÃO do município** (13/09/2026, pedido do Paulo: *"quero o brasão da
  prefeitura aí, no lugar desse desenho verde"*). Antes era um `+` branco em quadrado verde,
  desenhado em SVG dentro do próprio `<link>`. A arte veio do Wikimedia Commons
  (`BrasaoSaoMAteusDoSul.png`, 1213×1200, fundo transparente) porque nenhuma das marcas que já
  estavam aqui serve: nelas o brasão vem colado ao texto e mede no máximo 180 px de lado, e
  recortado ficaria sem resolução. O corte é a caixa do conteúdo com 10% de folga, centrado em
  quadrado; daí saem 16, 32, 48 e 180 px, os três primeiros empacotados em `favicon.ico`
  (PNG-in-ICO, montado à mão em PowerShell — não há ferramenta de imagem nesta máquina) e o de
  180 como `apple-touch-icon.png`. **Aos 16 px o brasão vira um borrão colorido**, e isso é da
  natureza dele: é um brasão heráldico completo, com espigas, milho, laço e três linhas de texto.
  Se um dia incomodar, o caminho é recortar só o escudo central — mas aí já não é o brasão
  inteiro.
- **O cartão inteiro é clicável**, não só o "Abrir": no celular, isso é a diferença entre
  acertar e errar o toque.
- **O endereço aparece por extenso** embaixo de cada bloco, porque quem divulga precisa
  poder ditá-lo por telefone.
- **No escuro o logotipo ganha uma placa branca.** Ele é colorido sobre fundo transparente;
  sem a placa, o azul do texto some no fundo escuro.
- **Cada link abre em aba nova** (`target="_blank"` + `rel="noopener"`), para a pessoa não
  perder a porta ao fechar o app.
- **Sem biblioteca, sem build.** Um `index.html`, as imagens e o `CNAME`.
- **As fontes moram no repositório, não no Google** (13/09/2026). Antes vinham do Google Fonts;
  isso custava duas conexões novas (DNS + TLS em `fonts.googleapis.com` e em `fonts.gstatic.com`)
  antes de o texto assentar — nos postos rurais, com sinal ruim, isso aparece — e fazia a página de
  uma secretaria de saúde chamar um terceiro a cada visita. Ficaram só os arquivos do subconjunto
  **latino** (`fontes/`, 68 KB somados): ele cobre `U+0000–00FF`, ou seja, todo acento do
  português; o `latin-ext` foi baixado e descartado (mais 92 KB para glifos que esta página nunca
  usa). Archivo e Source Sans 3 são licença SIL OFL, que permite hospedar.

## A altura da página, e por que ela não virou aba nem sanfona (13/09/2026)

O Paulo apontou que, no computador, era preciso rolar para achar os apps — *"muitas vezes pode ser
que nem ache"* — e perguntou se não dava para deixar mais dinâmico. **Não virou dinâmico de
propósito.** Com sete cartões, aba/sanfona/carrossel não facilita achar: esconde metade atrás de um
clique e obriga a pessoa a adivinhar em que gaveta está o que ela quer. O que sobrava era **altura
de cartão**, e foi o que caiu:

- **Saiu a linha "Abrir ↗"** de cada cartão. O cartão inteiro já era clicável desde o começo — a
  linha era enfeite custando ~50 px em cada um dos sete. A seta subiu para o canto do cartão: some
  a frase, fica o sinal de que abre em aba nova.
- **Quatro cartões por fileira** em vez de três, o que exigiu abrir o `main` de 980 para 1100 px.
  "Sistemas" inteiro passou a caber numa fileira.
- **"Documentos" e "Prefeitura" ficaram lado a lado** (`.duplas`, 1/3 e 2/3). Uma tem um cartão e a
  outra tem dois: sozinhas, gastavam duas fileiras inteiras para três cartões. Empilham no celular
  (abaixo de 760 px).

Resultado medido: a página caiu de ~1700 px para **1125 px** de altura, e o título "Prefeitura"
subiu para os 637 px — dentro da primeira tela de um notebook. No celular continua sendo rolagem
(sete cartões numa coluna são 2343 px), e é aceitável: lá a porta de entrada é o atalho na tela
inicial, não a rolagem.

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

## A troca de endereço (14/09/2026)

`guiaaps.com.br` → **`saudesaomateusdosul.com.br`**. O motivo é dele: *"o nome não combina mais"* —
o "aps" ficou apertado para o que a página virou (já tem Prefeitura, documentos, sistema da
Secretaria). O domínio ele mesmo registrou, no Registro.br, em nome próprio.

**`guiasaude.com.br` seria o nome óbvio e é de um terceiro** (registrado, vence em 2027). Ficaram
livres `guiasaude.org.br` e os `.net.br`/`.inf.br`/`.tec.br`, e a escolha entre "o nome da página
em .org.br" e "um nome do município em .com.br" foi dele.

### O que mudou de endereço, e o que NÃO mudou

**Só a raiz.** `planifica.guiaaps.com.br` e `documentos.guiaaps.com.br` continuam onde estavam,
apontando para a Vercel — são registros próprios na zona de `guiaaps.com.br`, e nada nesta troca
os alcança. **O domínio antigo continua sendo pago**, e por causa desses dois, não da porta.

### O antigo redireciona, e precisou de repositório próprio

O GitHub Pages aceita **um domínio por repositório** (é o que o arquivo `CNAME` diz). Com este
repositório respondendo pelo endereço novo, o antigo pararia de abrir — e ele está em grupo de
WhatsApp, no menu do Planifica Fácil e em rodapé de documento impresso. Por isso
**`paulosgp/guiaaps-redirecionamento`**: público, sem conteúdo, só uma página que redireciona,
com `CNAME` = `guiaaps.com.br`.

O redirecionamento é **duplo de propósito**: `<meta http-equiv="refresh">` funciona sem
JavaScript, e o `location.replace` leva caminho, query e âncora junto **e substitui** a entrada
no histórico — sem isso, o "voltar" do navegador devolveria a pessoa para a página de
redirecionamento, num laço.

### A ordem, que é o que impede a página de ficar sem endereço nenhum

1. os cinco registros na zona do domínio novo (4 × `A` do Pages + `CNAME` de `www`);
2. **esperar publicar de verdade** — conferido em dois resolvedores públicos, nunca no painel;
3. só então trocar o `CNAME` deste repositório;
4. criar o repositório de redirecionamento e ligar o Pages nele.

Trocar o `CNAME` antes do passo 2 derruba o endereço antigo na hora e o novo ainda não responde:
a página fica sem nenhum endereço funcionando. Entre o 3 e o 4 há uma janela de minutos em que a
raiz antiga devolve 404 — por isso os dois andam juntos, no mesmo dia.

### O que custou uma noite, e vale saber antes de abrir domínio novo no Registro.br

**Domínio recém-registrado entra numa janela de transição (~2 h) em que o editor de zona não
aplica nada.** Os cinco registros foram gravados, o painel os listou de volta depois de recarregar
a página — e **eles não publicaram**. Quatro horas depois a zona existia (SOA e NS respondendo) e
continuava **vazia**. Não era propagação: era o Registro.br não ter aplicado.

Duas coisas ficam disso: **conferir no DNS, nunca no painel** (`nslookup` contra 8.8.8.8 e
1.1.1.1 é a única prova de que publicou), e **contar com refazer os registros depois que a janela
fechar**. Ela se anuncia na própria tela ("Domínio em transição" e "o Modo básico só poderá ser
selecionado em aproximadamente 1h59m").

### O HTTPS não sai sozinho — e o jeito de saber é olhar a API, não tentar o endereço

Depois da virada, `https://` ficou **2h30 sem responder**. A documentação do GitHub diz "pode levar
até uma hora", então a primeira hora é espera normal. O que estava acontecendo era outra coisa: **o
pedido do certificado nunca tinha começado** — em `gh api repos/<dono>/<repo>/pages` não existia o
objeto `https_certificate`.

**Essa é a distinção que só a API dá.** Tentar o `https://` devolve exatamente o mesmo erro de
conexão nos dois casos — "ainda não foi pedido" e "está sendo emitido" —, então ficar recarregando
o navegador não diz nada. Na API:

| `https_certificate` | o que significa |
|---|---|
| ausente | **não começou** — é hora do empurrão |
| `authorization_pending` | está sendo emitido; esperar |
| `approved` | pronto, e aí dá para ligar o `https_enforced` |

**O empurrão é o que o próprio GitHub documenta:** tirar o domínio das configurações do Pages e pôr
de volta. Pela API são dois `PUT` — `{"cname":null}` e depois `{"cname":"<dominio>"}` —, e o estado
mudou para `authorization_pending` no mesmo minuto. **Não mande `https_enforced` junto no PUT de
remoção**: enquanto não há certificado, a API recusa a requisição inteira com "The certificate does
not exist yet" e nada acontece — parece que o comando rodou.

O site fica fora do ar por **segundos** entre os dois PUT (e só no domínio personalizado; o
`paulosgp.github.io/guia-saude` continua). O arquivo `CNAME` do repositório continua sendo a fonte
da verdade e é reaplicado na compilação seguinte.

**Ligar o `Enforce HTTPS` é um passo à parte, e não é automático**: `{"https_enforced":true}` depois
de `approved`. Sem ele, `http://` continua servindo a página em claro para sempre.

### O ícone da aba e o `apple-touch-icon` continuam sendo o brasão

Não mudaram com o domínio. Mudaram sim as metatags `og:` — apontavam para `guiaaps.com.br`, e é
delas que sai a prévia quando alguém manda o link no grupo.

## O atalho na tela do celular (14/09/2026)

Foi a primeira melhoria da lista que eu tinha proposto e ele aprovou, e é a que ataca o problema
real desta página: **uma porta só serve se as pessoas passarem por ela**. Quem tem de lembrar e
digitar o endereço volta a abrir o sistema que já está salvo no celular, e a porta não pega.

São duas peças: **`manifest.webmanifest`** (nome curto, `display: standalone`, o brasão em 192 e
512 — gerados do mesmo quadrado do favicon) e um **bloco no rodapé** com o passo a passo de
Android e iPhone.

**Fica no RODAPÉ, não no topo**: é coisa de fazer uma vez só, e no topo viraria ruído diário para
quem já instalou.

**Foi feito DEPOIS da troca de domínio, e a ordem não é detalhe:** atalho instalado guarda a
origem, então um atalho criado no endereço antigo viraria casca vazia depois da mudança — cada
pessoa teria de instalar de novo.

Os ícones **não são `maskable`** de propósito: o brasão tem fundo transparente e o recorte
circular do Android comeria as espigas e o laço. Como `any`, o sistema desenha a placa por baixo.

## Publicar uma mudança

Editar o `index.html`, commitar e dar push no `main`. O Pages publica sozinho em um ou dois
minutos. Não há build, não há painel, não há segredo em lugar nenhum.

**Para conferir no navegador antes de publicar**: abrir o arquivo por `file://` não serve — o
painel o carrega como `data:`, e aí todo `<img>` de caminho relativo some, dando a impressão falsa
de que os ícones quebraram. Há um servidor estático mínimo para isso em
`.claude apps/.claude/serve-guiasaude.js` (config `guiasaude` no `launch.json` da pasta raiz, porta
4173). Ele fica **fora** deste repositório de propósito: este aqui é público, e o servidor é
ferramenta de máquina, não parte do site. O caminho do node no `launch.json` está em formato 8.3 e
com barras normais (`C:/PROGRA~1/nodejs/node.exe`) porque o lançador engasga tanto com o espaço de
`Program Files` quanto com a contrabarra.

## O contato do rodapé (13/09/2026)

"Fale com a coordenação da Atenção Primária" não era acionável — a pessoa trava no celular e a
frase não leva a lugar nenhum. Virou um botão de WhatsApp (`wa.me/5542988724354`, **(42)
98872-4354**, número dado pelo Paulo), com o número por extenso ao lado para quem estiver no
computador e precisar anotar ou ligar. **Sem o logotipo do WhatsApp**: a palavra já identifica, e a
marca é de terceiro — mesmo critério que segurou o ícone do SIGSS e o do Oxy.


## Encaminha APS (cartão desde 14/09/2026)

Quinto cartão de "Sistemas", logo depois do Planifica Fácil: é o app irmão dele (mesma stack,
mesmo login), então fica ao lado. Leva a `encaminha.guiaaps.com.br` — o domínio já está no
projeto da Vercel; enquanto o Paulo não criar o CNAME no Registro.br, o endereço que responde
é `encaminha.vercel.app`, e o cartão fica apontando para o definitivo de propósito (trocar
depois custaria uma segunda edição e a equipe decoraria o provisório). Ícone
`logo-encaminha.svg`, nosso: duas setas que se cruzam (referência e contrarreferência) no
rosa que o Paulo escolheu para o app; o mesmo arquivo é o favicon dele
(`Encaminha/src/app/icon.svg`). Rótulo "Médicos, enfermeiros e o Centro de Ginecologia":
são os dois lados que entram — ACS e técnicos da unidade não têm conta lá.

**O endereço definitivo passou a funcionar em 21/09/2026**, quando o CNAME `encaminha` foi criado na zona de `guiaaps.com.br` e propagou. Durante algumas horas daquele dia o cartão apontou para `encaminha.vercel.app`, porque o link definitivo estava morto — link morto é pior que endereço provisório. Já voltou para `encaminha.guiaaps.com.br`.

**Selo "Em construção" (15/09/2026).** O Paulo pediu que o cartão avisasse que o app ainda não é
para uso da rede: os 16 protocolos aguardam a revisão das especialistas, as contas das unidades
e do Centro não foram criadas, e o DNS ainda não estava feito. O link continua vivo de propósito
(quem for testar entra por ali); o que muda é o selo âmbar abaixo do nome (classe `.selo`,
numa linha própria — dentro do cabeçalho do cartão ele era cortado na largura de 4 colunas),
a borda tracejada (`.app.construcao`) e a frase final da descrição, "aguarde o aviso da
coordenação antes de usar". O âmbar é deliberado: o chip verde já significa "quem usa", e um
aviso da mesma cor passaria batido. Quando o app for liberado, remover as três coisas — o selo,
a classe `construcao` e a frase — e nada mais.
