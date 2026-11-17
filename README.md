# Guia Completo do Projeto Estúdio BDD (para Iniciantes)

---

## Parte 1: O que é BDD? (Explicado do zero)

Imagine que você quer pedir para alguém construir uma **máquina de fazer suco** (ou um aplicativo de celular).
Se você disser só: *"Faz uma máquina de suco boa!"*, a pessoa pode fazer errado.

Então, no mundo da computação, as equipes usam duas coisas juntas:

1. **História de Usuário** — É um cartão curto que explica **quem** quer, **o que** quer e **para quê**:
   > **Como** um cliente com sede,
   > **Quero** colocar moedas e escolher o sabor de laranja,
   > **Para** receber meu copo de suco gelado.

2. **BDD (Desenvolvimento Guiado por Comportamento)** — É um jeito de escrever **exemplos concretos** de como o sistema tem que funcionar, usando português bem simples, quase como uma receita de bolo com 3 palavras mágicas:
   - **DADO** *(como tudo começa / o cenário inicial)*
   - **QUANDO** *(o que a pessoa faz / o clique ou ação)*
   - **ENTÃO** *(o resultado que tem que acontecer na tela)*

   Exemplo de um **Cenário BDD**:
   ```gherkin
   Cenário: Compra de suco com dinheiro suficiente
     Dado que a máquina tem suco de laranja disponível
     Quando o cliente coloca 5 reais e aperta o botão Laranja
     Então a máquina entrega o copo de suco
   ```

   Se precisar continuar uma frase, usamos **E** ou **MAS** (por exemplo: *"E exibe a mensagem Obrigado!"*).
   > **Regra de ouro:** você nunca começa uma receita dizendo *"E mexa a massa"* sem antes ter dito o início, certo? No BDD é igual: **E** e **MAS** nunca podem ser o primeiro passo, e os passos sempre seguem a ordem **DADO → QUANDO → ENTÃO**.

3. **Arquivo `.feature`** — Quando essas histórias e cenários ficam prontos, nós juntamos tudo em um arquivo de texto terminado em `.feature`. Ferramentas profissionais (como o *Cucumber*) conseguem ler esse arquivo e testar o programa automaticamente!

---

## Parte 2: Qual é o objetivo do site Estúdio BDD?

O **Estúdio BDD** é um site feito para **escrever e organizar essa documentação de requisitos**, com ajuda de **Inteligência Artificial (IA)** — mas com o **humano mandando no final**.

A frase principal do projeto é: **"A IA rascunha, o humano decide."**

- O site **NÃO** tem um robô de IA conectado dentro dele.
- O analista (você) abre o Gemini ou ChatGPT em outra aba, pede ideias de cenários novos para uma história e **registra no site** o que a IA respondeu (qual ferramenta usou, qual pergunta/prompt fez e qual foi a resposta).
- Depois, o **autor da história** lê a sugestão da IA e decide:
  - **ACEITAR:** *"Boa ideia!"* (mas o site não cria o cenário sozinho; o humano vai lá, escreve/ajusta o cenário com cuidado e marca que a origem veio de `IA_ACEITA`).
  - **REJEITAR:** *"Ideia ruim!"* — e o sistema **obriga** a dizer o motivo (`INCORRETA`, `GENERICA`, `DUPLICADA`, `FORA_DO_ESCOPO` ou `OUTRO`) e escrever uma justificativa. Assim fica registrado no histórico quando a IA ajudou e quando ela atrapalhou.
- Só quando **não sobrar nenhuma sugestão pendente** (e a história tiver pelo menos 1 cenário) é que o site deixa **baixar o arquivo `.feature`**.

---

## Parte 3: Qual é o fluxo completo do site? (Passo a passo)

```
[1. Escolher Usuário] ──▶ [2. Escolher Projeto] ──▶ [3. Criar História (Como/Quero/Para)]
                                                                 │
                                                                 ▼
[6. Baixar .feature] ◀── [5. Curadoria: Aceitar/Rejeitar] ◀── [4. Escrever Cenários + Registrar Ideia da IA]
        │
        ▼
[7. Ver Resumo com Gráficos/Números do Projeto]
```

Passo a passo na prática:
1. **Identificação (Topo do site):** Você escolhe quem você é no menu **"Usuário de Demonstração"** (ex.: *#1 Gabriel* ou *#2 Kauê*). Como o trabalho não pede tela de login com senha, o site envia esse número em um cabeçalho invisível chamado `X-Usuario-Id` para saber se você é o dono da história.
2. **Aba 6 (Usuários & Projetos):** Se quiser, cadastre mais pessoas e crie um **Projeto** (ex.: *"Loja Virtual"*), dando nome, descrição e contexto (glossário).
3. **Aba 1 (Projetos & Histórias):** Crie uma **História de Usuário** (Título, Como, Quero, Para, Prioridade). Na direita, veja a lista de histórias com quantos cenários e quantas sugestões pendentes cada uma tem, podendo **filtrar por prioridade** (`ALTA`, `MEDIA`, `BAIXA`), **Abrir**, **Editar** ou **Excluir**.
4. **Aba 2 (Cenários & Passos BDD):** Com a história selecionada, escreva os **Cenários** dela adicionando passos (`DADO`, `QUANDO`, `ENTAO`, `E`, `MAS`). Você pode mover passos para cima (`↑`) e para baixo (`↓`), editar cenários existentes ou excluir.
5. **Aba 3 (Sugestões de IA & Curadoria):** De um lado aparece a **História** para você consultar; do outro aparece a **Fila de Curadoria**. Você registra uma sugestão da IA (ela nasce `PENDENTE`), e depois o autor da história **Aceita** ou **Rejeita** (com motivo e justificativa).
6. **Aba 4 (Exportar .feature):** Clica em **Validar & Visualizar .feature**. Se estiver tudo ok, aparece o texto Gherkin pronto e você pode baixar o arquivo `.feature`.
7. **Aba 5 (Resumo do Projeto):** Mostra o painel de números do projeto: total de histórias, cenários feitos por humanos vs. IA, sugestões pendentes/aceitas/rejeitadas e os motivos pelos quais a IA mais errou.

---

## Parte 4: Roteiro de Testes para Você Fazer no Site Agora

Com a aplicação rodando, abra **`http://localhost:8080`** no navegador e faça estes 10 testes (eles cobrem todas as regras exigidas pelo professor no PDF!):

### Teste 1 — Dados iniciais carregados automaticamente
- **O que olhar:** No topo do site, veja se o seletor de Usuário mostra `#1 Gabriel Gomes` e o Projeto mostra `#1 Portal Acadêmico Mackenzie`, e na Aba 1 aparecem 2 histórias (*Autenticação de Aluno* e *Solicitação de Trancamento*).
- *Obs.: Se o seu banco Supabase já tinha dados de antes, pode aparecer apenas 1 usuário; nesse caso, crie um 2º usuário na Aba 6 para testar o Teste 5!*

### Teste 2 — Criar história e testar título repetido (Regra 1)
1. Na **Aba 1**, preencha uma nova história (ex.: Título *"Recuperar Senha"*, Como *"aluno"*, Quero *"redefinir minha senha"*, Para *"voltar a acessar o portal"*, Prioridade `MEDIA`) e clique em **Salvar História**.
2. Tente criar **outra** história com o **mesmo título** *"Recuperar Senha"* no mesmo projeto.
3. **Esperado:** O site deve bloquear com erro vermelho (409 Conflict) dizendo que já existe história com esse título no projeto.

### Teste 3 — Regras do BDD ao criar cenário (Regra 2)
1. Selecione a história *"Recuperar Senha"* (botão **Abrir**) e vá para a **Aba 2 (Cenários & Passos BDD)**.
2. **Teste inválido 1 (sem ENTAO):** Remova o passo `ENTAO` (clique no `X` vermelho) e tente salvar. **Esperado:** Erro dizendo que precisa de ao menos um passo `ENTAO`.
3. **Teste inválido 2 (começar com E):** Mude o primeiro passo para `E` e tente salvar. **Esperado:** Erro dizendo que `E` ou `MAS` não podem iniciar o cenário.
4. **Teste inválido 3 (fora de ordem):** Coloque `QUANDO` antes de `DADO` e tente salvar. **Esperado:** Erro dizendo que `DADO` não pode aparecer após `QUANDO`.
5. **Teste válido:** Deixe `DADO` → `QUANDO` → `ENTAO` e salve. **Esperado:** Cenário salvo e listado à direita!

### Teste 4 — Editar cenário e reordenar passos (Item 3 do roteiro do PDF)
1. Na **Aba 2**, clique em **Editar / Reordenar Passos** em um cenário existente.
2. Adicione um novo passo `E`, use os botões **`↑`** e **`↓`** para posicioná-lo logo após o `ENTAO`, e salve.
3. Atualize a página (`F5`) e confira se os passos continuaram na ordem exata em que você deixou.

### Teste 5 — Bloqueio de quem NÃO é o autor (Regra 3 — `X-Usuario-Id`)
1. Na **Aba 6**, cadastre um 2º usuário (ex.: *"Maria"*, `maria@mackenzie.br`), caso ainda não exista um 2º usuário.
2. No seletor **Usuário de Demonstração** no topo da tela, troque para esse 2º usuário.
3. Tente **Editar** ou **Excluir** a história *"Autenticação de Aluno no Portal"* (cujo autor é o Gabriel `#1`).
4. **Esperado:** Erro vermelho (403 Forbidden): *"Somente o autor da história pode editar/excluir..."*.

### Teste 6 — Registrar sugestão de IA e testar rejeição sem motivo (Regra 4)
1. Volte no topo para o usuário `#1 Gabriel` e abra a história *"Solicitação de Trancamento de Disciplina"*.
2. Vá na **Aba 3 (Sugestões de IA & Curadoria)**. Veja que a história aparece à esquerda e a fila à direita.
3. Na sugestão `PENDENTE` que já existe, clique em **Rejeitar Sugestão**, deixe a justificativa **em branco** e clique em **Confirmar Rejeição**.
4. **Esperado:** Bloqueio! A justificativa é obrigatória.
5. Agora escreva uma justificativa (ex.: *"Já coberto em outra história"*) e rejeite.
6. **Esperado:** Status muda para `REJEITADA`. Os botões de decisão somem (pois uma sugestão já decidida **nunca mais pode ser alterada**).

### Teste 7 — Aceitar sugestão NÃO cria cenário sozinho (Regra 4)
1. Ainda na **Aba 3**, registre uma nova sugestão de IA (Ferramenta: `ChatGPT`, Prompt e Conteúdo quaisquer). Ela nascerá `PENDENTE`.
2. Clique em **Aceitar Sugestão** e confirme.
3. **Esperado:** Ela vira `ACEITA`, e o número de cenários **não muda sozinho**. Aparece o botão *"Criar/Ajustar Cenário com origem IA_ACEITA"*, que leva você à Aba 2 para cadastrar o cenário manualmente com a origem `IA_ACEITA`.

### Teste 8 — Bloqueio e sucesso da exportação `.feature` (Regra 5)
1. Em uma história que tenha uma sugestão `PENDENTE` (ou nenhum cenário), vá na **Aba 4** e clique em **Validar & Visualizar .feature**.
   - **Esperado:** Caixa vermelha dizendo *"BLOQUEIO DE GOVERNANÇA"*.
2. Selecione a história #1 (*Autenticação de Aluno no Portal*) e clique em **Validar & Visualizar .feature**.
   - **Esperado:** Aparece o texto azul começando com `# language: pt`, `Funcionalidade:`, `Como`, `Quero`, `Para` e os cenários. Clique em **Baixar Arquivo (.feature)** para fazer o download.

### Teste 9 — Filtro por prioridade e Resumo do Projeto (Regras 6 e 7)
1. Na **Aba 1**, mude o filtro para `ALTA` e depois `MEDIA` e confira se a lista filtra corretamente e mostra as contagens de cenários e pendências.
2. Na **Aba 5 (Resumo do Projeto)**, confira se os números de histórias, cenários (`HUMANO` vs `IA_ACEITA`), sugestões e motivos de rejeição batem com o que você cadastrou.

### Teste 10 — Persistência (Item 9 do roteiro do PDF)
- Pare o servidor no terminal (`Ctrl + C`), inicie de novo e dê `F5` no navegador. Tudo que você cadastrou deve continuar lá (salvo no PostgreSQL/Supabase).

---

## Parte 5: Para que serve cada arquivo do projeto

Abaixo está a lista de todos os arquivos do projeto, agrupados por pasta (camada). Pense em um prédio onde cada andar tem uma responsabilidade:

### 1. Arquivos da Raiz e Configuração
| Arquivo | Para que serve |
|---|---|
| `pom.xml` | É a "lista de compras" do projeto (Maven). Diz qual versão do Java (17) e quais bibliotecas externas usamos (Spring Boot Web, JPA para banco, Validation, PostgreSQL, Swagger e ArchUnit). |
| `application.properties` | Arquivo de configurações: porta do servidor (`8080`), endereço/usuário/senha do banco PostgreSQL (Supabase) e opção `ddl-auto=update` (cria/atualiza as tabelas automaticamente). |
| `EstudioBddApplication.java` | É o botão de "Ligar" do backend (`main`). Quando você roda essa classe, o Spring Boot sobe o servidor web na porta 8080. |
| `CorsConfig.java` | É o "porteiro" do navegador: diz quais endereços de site (`http://localhost:8080`, etc.) têm permissão para enviar requisições para a API e usar o cabeçalho `X-Usuario-Id`. |
| `DataSeeder.java` | Roda automaticamente quando o servidor liga. Se a tabela de usuários estiver vazia, ele cria dados de exemplo (2 usuários, 1 projeto, 2 histórias, 1 cenário e 1 sugestão) para ninguém começar com a tela em branco. |
| `AGENTS.md` | Diário de bordo exigido pelo professor: registra as regras do projeto e pelo menos 6 interações de desenvolvimento feitas com apoio de IA. |
| `README.md` | Manual de apresentação do projeto (integrantes, como rodar, endpoints). |

### 2. Camada `model/` — As Tabelas do Banco de Dados
Cada classe aqui vira uma **tabela** no PostgreSQL (usando `@Entity`):
| Arquivo | Tabela / Papel |
|---|---|
| `Usuario.java` | Tabela `usuarios`: guarda `id`, `nome` e `email` (único). É quem cria projetos, escreve histórias e avalia sugestões. |
| `Projeto.java` | Tabela `projetos`: guarda `nome` (único), `descricao`, `contextoDominio` (glossário), `dataCriacao` e quem criou. Tem uma lista de `HistoriaUsuario`. |
| `HistoriaUsuario.java` | Tabela `historias_usuario`: guarda `titulo` (único dentro do projeto), `papel` (*Como*), `acao` (*Quero*), `beneficio` (*Para*), `prioridade`, datas, o `projeto` e o `autor`. Possui cenários e sugestões. |
| `Cenario.java` | Tabela `cenarios`: guarda `titulo` (único dentro da história), `posicao`, `origem` (`HUMANO` ou `IA_ACEITA`) e a lista ordenada de `Passo`. |
| `Passo.java` | Tabela `passos`: guarda `tipo` (`DADO`, `QUANDO`, `ENTAO`, `E`, `MAS`), `texto` e `ordem` (1, 2, 3…). Pertence exclusivamente a um `Cenario`. |
| `Sugestao.java` | Tabela `sugestoes`: guarda `ferramenta`, `prompt`, `conteudo`, `decisao`, `motivoRejeicao`, `justificativa`, datas, quem registrou e quem decidiu. |
| `Prioridade.java`, `OrigemCenario.java`, `TipoPasso.java`, `DecisaoSugestao.java`, `MotivoRejeicao.java` | São `enum`s: listas fechadas de opções válidas (para ninguém digitar uma prioridade inventada como `"URGENTÍSSIMA"`). |

### 3. Camada `repository/` — Quem conversa com o Banco
São interfaces (`extends JpaRepository`) onde o Spring gera o SQL sozinho. Não têm regras de negócio, apenas buscas e contagens:
| Arquivo | O que faz |
|---|---|
| `UsuarioRepository.java` | Busca usuário por e-mail e verifica se um e-mail já existe. |
| `ProjetoRepository.java` | Lista projetos, busca por nome e verifica nome duplicado (inclusive na edição). |
| `HistoriaUsuarioRepository.java` | Lista histórias do projeto (com ou sem filtro de prioridade), conta histórias e checa título duplicado no projeto. |
| `CenarioRepository.java` | Lista cenários em ordem de `posicao`, checa título duplicado na história e conta cenários por origem (`HUMANO` vs `IA_ACEITA`) para o resumo. |
| `PassoRepository.java` | Busca passos ordenados por `ordem`. |
| `SugestaoRepository.java` | Lista sugestões por história/decisão, verifica se existe sugestão `PENDENTE` (para bloquear exportação) e agrupa contagens/motivos para o resumo. |

### 4. Camada `dto/` — Os "Formulários" de Entrada e Saída
Em Java moderno usamos `record` (objetos simples e imutáveis que só carregam dados) para nunca expor as tabelas do banco direto na internet:
| Arquivo | Para que serve |
|---|---|
| `UsuarioRequestDTO` / `UsuarioResponseDTO` | Entrada (valida `@NotBlank` e `@Email`) e saída de usuário. |
| `ProjetoRequestDTO` / `ProjetoResponseDTO` | Entrada (valida tamanho de nome/descrição) e saída de projeto. |
| `HistoriaUsuarioRequestDTO` / `HistoriaUsuarioResponseDTO` | Entrada e saída completa de uma história. |
| `HistoriaResumoDTO` | Linha resumida da história para a lista do projeto (inclui `qtdCenarios` e `qtdSugestoesPendentes`). |
| `ResumoProjetoDTO` | Dados do painel de métricas (totais, mapas por origem/decisão e lista de motivos de rejeição). |
| `CenarioRequestDTO` / `CenarioResponseDTO` / `PassoDTO` | Entrada e saída de cenários com seus passos ordenados. |
| `SugestaoRequestDTO` / `SugestaoResponseDTO` | Entrada e saída do registro de sugestões de IA. |
| `CuradoriaRequestDTO` | Entrada da decisão humana (`decisao`, `motivoRejeicao`, `justificativa`). |
| `ErroRespostaDTO` | Classe legada da versão antiga de erros (atualmente o sistema usa `ProblemDetail` padrão do Spring). |

### 5. Camada `service/` — O Cérebro (Regras de Negócio)
Aqui ficam todas as regras do PDF:
| Arquivo | Responsabilidades |
|---|---|
| `RegrasAutoria.java` | Helper que confere se o ID do usuário atual (`X-Usuario-Id`) é o mesmo ID do autor da história. Se não for, lança `AcessoNegadoException` (erro 403). |
| `UsuarioService.java` | Cadastra usuário garantindo e-mail único, lista e busca por ID. |
| `ProjetoService.java` | Cria, edita, exclui projetos (garantindo nome único e checando o dono) e calcula o `ResumoProjetoDTO`. |
| `HistoriaUsuarioService.java` | Cria, edita, exclui histórias (checando título único no projeto e autoria), consulta histórias com contagens/filtro e **gera o texto `.feature`**. |
| `CenarioService.java` | Cria, edita e exclui cenários e passos individuais, reorganiza posições e **valida a sintaxe BDD** (`DADO → QUANDO → ENTAO`, mínimo 1 `QUANDO` e 1 `ENTAO`, sem `E`/`MAS` no início). |
| `SugestaoService.java` | Registra sugestões como `PENDENTE`, realiza a curadoria (bloqueia alteração após decisão, exige motivo e justificativa ao rejeitar, valida autoria) e lista por história/decisão. |

### 6. Camada `controller/` e `exception/` — A Porta de Entrada da API e Tratamento de Erros
| Arquivo | Responsabilidades |
|---|---|
| `IdentidadeSimulada.java` | Define a constante `CABECALHO = "X-Usuario-Id"` e documenta que isso é apenas uma simulação acadêmica (não é login real). |
| `UsuarioController.java` | Endpoints `/api/usuarios` (`POST`, `GET`). |
| `ProjetoController.java` | Endpoints `/api/projetos` (`POST`, `GET`, `PUT`, `DELETE`), `/api/projetos/{id}/historias` (consulta com filtro) e `/api/projetos/{id}/resumo`. |
| `HistoriaUsuarioController.java` | Endpoints `/api/historias` (`POST`, `GET`, `PUT`, `DELETE`) e `/api/historias/{id}/exportar-feature`. |
| `CenarioController.java` | Endpoints `/api/cenarios` (`POST`, `GET`, `PUT`, `DELETE`) e `/api/cenarios/{id}/passos` (`GET`, `POST`, `PUT`, `DELETE`). |
| `SugestaoController.java` | Endpoints `/api/sugestoes` (`POST`, `GET`) e `/api/sugestoes/{id}/curadoria` (`PATCH`). |
| `RecursoNaoEncontradoException`, `RegraNegocioException`, `ConflitoException`, `AcessoNegadoException` | Exceções personalizadas para separar cada tipo de erro. |
| `GlobalExceptionHandler.java` | Intercepta qualquer erro no projeto (`@RestControllerAdvice`) e transforma em um JSON `ProblemDetail` padronizado com o código HTTP certo (`400`, `403`, `404`, `409`, `422`, `500`). |

### 7. Frontend (SPA) e Testes Automatizados
| Arquivo | Responsabilidades |
|---|---|
| `src/main/resources/static/index.html` | Toda a tela do site (HTML + CSS + JavaScript). Faz chamadas `fetch` para `/api/...` enviando o cabeçalho `X-Usuario-Id` do usuário selecionado no topo. |
| `ArquiteturaCamadasTest.java` | Teste **ArchUnit**: verifica automaticamente se nenhum `Controller` está acessando `Repository` direto e se nenhum `Service` depende de `Controller`. |
| `EstudioBddRegrasTest.java` e `RegrasNegocioTest.java` | Testes **JUnit 5 + Mockito**: testam as regras de negócio na memória (sem precisar do banco) — cenário sem `ENTAO`, cenário começando com `E`, ordem inválida, rejeição sem motivo, decisão imutável, autoria e bloqueio de exportação. |
| `EstudioBddApplicationTests.java` | Teste padrão do Spring Boot (`contextLoads`) que verifica se a aplicação inteira sobe (este conecta no banco configurado no `application.properties`). |

---

## Parte 6: Verificação dos Requisitos do PDF (`Projeto_PS2_Estudio_BDD.pdf`)

| Requisito do PDF | Situação Atual | Observação |
|---|---|---|
| **Arquitetura em 5 camadas** (`Controller → DTO → Service → Repository → Model`) + injeção por construtor + ArchUnit | ✅ **Cumprido** | `ArquiteturaCamadasTest` garante a separação de camadas. |
| **Regra 1:** Unicidade (e-mail, nome do projeto, título da história no projeto) e campos obrigatórios | ✅ **Cumprido** | Validado nos Services, DTOs (`@Valid`) e restrições `UNIQUE` no banco. |
| **Regra 2:** Cenário válido (título único, ≥1 `QUANDO` e `ENTAO`, ordem `Dado→Quando→Então`, `E`/`MAS` não iniciam) | ✅ **Cumprido** | Validado em `CenarioService.validarEOrdenarPassos` (tanto na criação quanto na edição/reordenação). |
| **Regra 3:** Somente o autor edita/exclui história e cenários (usando cabeçalho `X-Usuario-Id`) | ✅ **Cumprido** | `RegrasAutoria` valida `X-Usuario-Id` em histórias, cenários, passos e curadoria. |
| **Regra 4:** Sugestão nasce `PENDENTE`, rejeição exige motivo, decisão imutável, aceitar **não** altera cenários automaticamente | ✅ **Cumprido** | Corrigido em `SugestaoService` e na SPA (`index.html`). |
| **Regra 5:** Exportação `.feature` em Gherkin `# language: pt`, só com ≥1 cenário e sem pendentes | ✅ **Cumprido** | `HistoriaUsuarioService.exportarFeature`. |
| **Regra 6:** Consulta do projeto listando histórias com qtd. cenários, qtd. pendentes e filtro por prioridade | ✅ **Cumprido** | `GET /api/projetos/{id}/historias?prioridade=...` + Aba 1 da SPA. |
| **Regra 7:** Resumo do projeto (histórias, cenários por origem, sugestões por decisão, motivos de rejeição) | ✅ **Cumprido** | `GET /api/projetos/{id}/resumo` + Aba 5 da SPA. |
| **Testes obrigatórios:** 3 testes de regras + ArchUnit | ✅ **Cumprido** | Presentes em `EstudioBddRegrasTest`, `RegrasNegocioTest` e `ArquiteturaCamadasTest`. |
| **SPA com as 6 telas mínimas + CORS restrito à origem da SPA** | ✅ **Cumprido** | Todas as 6 telas em `index.html`; `CorsConfig` restrito a `localhost:8080` / `127.0.0.1:8080`. |
| **Documentação e `AGENTS.md` com ≥6 interações** | ✅ **Cumprido** | `AGENTS.md` atualizado com 6 interações e limitação do `X-Usuario-Id`. |
| **Atividade Bônus (Seção 10 — Fluxo configurável / Kanban)** | ⚪ **Não implementada** | Item **opcional** no PDF. |

### Checklist final antes de entregar no Moodle (17/11/2026)
1. Rodar `.\mvnw.cmd test` e `.\mvnw.cmd spring-boot:run` no seu terminal para confirmar que todos os testes passam e o Swagger (`/swagger-ui.html`) abre.
2. **Remover a senha do banco** (`spring.datasource.password`) de `src/main/resources/application.properties` antes de compactar o ZIP (o PDF proíbe credenciais no entregável!).
3. Verificar se estão no repositório/ZIP: `README.md` atualizado com instruções para API/SPA/banco e limitação do `X-Usuario-Id`, diagrama de classes, um `.feature` exportado pelo sistema, `AGENTS.md`, roteiro/evidências de verificação, e **sem** a pasta `target/`.
