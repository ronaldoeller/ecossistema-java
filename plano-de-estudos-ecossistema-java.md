# Plano de Estudos: De Analista de Sistemas para Desenvolvedor Java Full Stack

**Contexto:** Você já trabalha com gestão de projetos e requisitos em uma stack Java Spring Boot + Angular + Oracle + IBM MQ + Redis. Isso é uma vantagem enorme — você já conhece os fluxos de negócio, a arquitetura geral e o vocabulário técnico. O plano abaixo foca em transformar esse conhecimento passivo em habilidade prática de codificação.

**Duração estimada:** 6 a 9 meses, estudando de 8 a 12h por semana (ajuste conforme sua disponibilidade).

**Metodologia:** cada fase combina teoria curta + prática imediata. Você só avança de fase quando conseguir construir algo funcional sozinho, sem copiar tutorial passo a passo.

---

## Ferramentas de Desenvolvimento (IDEs)

Antes de começar a Fase 0, vale configurar bem o ambiente — isso evita fricção desnecessária ao longo de todo o plano.

**IntelliJ IDEA (backend — Java/Spring Boot)**
- É a IDE de fato padrão de mercado para Java/Spring, amplamente preferida sobre Eclipse ou NetBeans na maioria das empresas hoje
- Versão **Community** (gratuita) já cobre praticamente tudo que você precisa nas Fases 0 a 3; a versão **Ultimate** (paga, mas com licença gratuita para estudantes e trials) adiciona suporte nativo a Spring Boot (visualização de beans, endpoints REST navegáveis), banco de dados integrado e suporte a JavaScript/Angular — vale considerar quando chegar nas fases mais avançadas
- Plugins essenciais: Lombok (reduz boilerplate em Java, muito usado em projetos Spring), SonarLint (feedback do Sonar direto na IDE, conecta com a Fase 3.75), .env/dotenv se for usar variáveis de ambiente
- Recursos a explorar desde cedo: debugger visual, refatorações automáticas (extrair método, renomear com segurança — conecta direto com a Fase 1.5 de Clean Code), atalhos de navegação (`Ctrl+Click`, `Ctrl+Shift+F`), Git integrado (commits, branches e resolução de conflitos direto na IDE)
- Templates de projeto: usar o **Spring Initializr integrado** (File → New → Project → Spring Boot) para começar cada novo projeto/serviço da forma padrão de mercado

**VS Code (frontend — Angular/TypeScript)**
- É a IDE mais usada no ecossistema frontend hoje, inclusive por times Angular, por ser leve e ter um ecossistema de extensões muito forte
- Extensões essenciais: **Angular Language Service** (autocomplete e checagem de tipos em templates HTML do Angular), **ESLint** (conecta direto com a Fase 3.75 de qualidade de código), **Prettier** (formatação automática, padrão de mercado para times frontend), **GitLens** (histórico e blame do Git direto no editor)
- Terminal integrado: usar para rodar `ng serve`, `ng generate` e os comandos do Angular CLI sem sair da IDE
- Configuração de `settings.json` do workspace para formatar automaticamente ao salvar (`"editor.formatOnSave": true`) — hábito que já emula o que times profissionais configuram como padrão de projeto

**Observação prática:** é comum, mesmo em times mais avançados, usar as duas IDEs simultaneamente ao trabalhar em um projeto full stack — IntelliJ com o backend aberto em uma janela, VS Code com o frontend aberto em outra. Vale já se acostumar com esse fluxo de alternar entre as duas desde as primeiras fases práticas.

---

## Fase 0 — Fundamentos sólidos (3 a 4 semanas)

Antes de Spring Boot, é preciso dominar Java puro e lógica de programação, senão você aprende "receita de bolo" sem entender o forno.

**Tópicos:**
- Sintaxe Java: tipos, coleções (List, Map, Set), streams e lambdas (Java 8+)
- Programação orientada a objetos: herança, interfaces, polimorfismo, classes abstratas
- Tratamento de exceções (checked vs unchecked)
- Generics
- Git: branching (Gitflow ou trunk-based), rebase vs merge, resolução de conflitos, pull requests

**Prática recomendada:**
- Exercícios em [LeetCode (fácil)](https://leetcode.com) ou [HackerRank Java track](https://www.hackerrank.com/domains/java)
- Criar um repositório Git pessoal e praticar fluxo completo: branch → commit → PR → merge

**Recursos comuns no mercado:**
- Livro: *Java: Como Programar* (Deitel) ou *Effective Java* (Bloch) — este último é referência de mercado para código "sênior"
- Curso: "Java Completo" (Nélio Alves, Udemy) — muito usado no Brasil

**Critério de avanço:** conseguir resolver problemas de lógica com streams (`filter`, `map`, `collect`) sem consultar.

---

## Fase 1 — Spring Boot (Backend) (6 a 8 semanas)

Aqui você entra na tecnologia central do seu ecossistema atual.

**Tópicos essenciais:**
- Spring Core: Inversão de Controle (IoC) e Injeção de Dependência (DI)
- Spring Boot: auto-configuração, `application.yml`/`properties`, profiles (dev/hml/prod)
- Spring Web (REST): controllers, `@RequestMapping`, DTOs, validação (`@Valid`, Bean Validation)
- Spring Data JPA: repositories, entidades, relacionamentos (`@OneToMany`, `@ManyToOne`), queries derivadas e `@Query`
- Arquitetura em camadas: Controller → Service → Repository (e variações como Hexagonal/Clean Architecture, comuns em projetos governamentais por exigência de manutenibilidade)
- Tratamento global de exceções (`@ControllerAdvice`)
- Segurança básica: Spring Security, JWT (muito comum em APIs governamentais com autenticação centralizada, tipo gov.br)
- Logs estruturados (SLF4J + Logback)

**Prática recomendada:**
- Construir uma API REST completa de CRUD (ex: sistema de gestão de solicitações, parecido com o que você já especifica)
- Depois, adicionar autenticação JWT e paginação/filtros

**Recursos comuns no mercado:**
- Documentação oficial: [spring.io/guides](https://spring.io/guides)
- Curso: "Spring Boot 3 - Do Zero à Maestria" ou similares (Udemy/Alura)
- YouTube: canal da Rocketseat e DevDojo têm boas trilhas gratuitas em pt-BR

**Critério de avanço:** ter uma API funcional no ar (local) com endpoints REST, validação e persistência real em banco.

---

## Fase 1.5 — Clean Code e Boas Práticas (2 a 3 semanas)

Este é o momento certo para essa fase: você já tem código funcionando (Fase 1) e agora vai aprender a deixá-lo **legível, testável e fácil de manter**. Fazer isso cedo evita criar vícios de código que depois são difíceis de desaprender.

**Tópicos:**
- Princípios de Clean Code: nomes significativos, funções pequenas e com uma única responsabilidade, comentários (quando são úteis e quando são "desculpa" para código ruim)
- SOLID aplicado a Java/Spring: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion — com exemplos práticos de como o próprio Spring já induz boas práticas via injeção de dependência
- Code smells comuns: métodos gigantes, classes "Deus" (God Object), duplicação de código, acoplamento excessivo
- Refatoração segura: como melhorar código existente com testes como rede de segurança (por isso a Fase 3 de testes vem logo depois)
- Design patterns mais usados no dia a dia Java/Spring: Strategy, Factory, Builder, Repository (que você já usa via Spring Data), Adapter
- Convenções de nomenclatura e organização de pacotes por feature vs por camada (debate comum em arquitetura Spring)

**Prática recomendada:**
- Pegar a API construída na Fase 1 e refatorá-la aplicando os princípios acima: quebrar métodos grandes, extrair interfaces, remover duplicação
- Fazer um "antes e depois" documentado — ótimo material para portfólio e para discutir em entrevistas técnicas

**Recursos comuns no mercado:**
- Livro: *Clean Code* (Robert C. Martin) — leitura praticamente obrigatória no mercado, mesmo com ressalvas que devs experientes fazem sobre alguns exemplos datados
- Livro: *Refactoring* (Martin Fowler) — para aprofundar depois
- Canal/curso: conteúdos sobre SOLID em Java (Rocketseat, Alura e vários vídeos gratuitos no YouTube em pt-BR)

**Critério de avanço:** conseguir olhar para um código com método muito longo ou muita responsabilidade misturada e saber, na hora, como quebrá-lo.

---

## Fase 2 — Oracle Database e JPA avançado (3 a 4 semanas)

Você já conhece o modelo de dados do seu sistema atual — hora de manipulá-lo via código.

**Tópicos:**
- SQL avançado no Oracle: joins, subqueries, window functions, procedures/functions PL/SQL básico
- JPA/Hibernate: lazy vs eager loading, N+1 problem, `@Transactional`, isolamento de transações
- Migrations com Flyway ou Liquibase (prática de mercado quase obrigatória para versionar schema)
- Connection pooling (HikariCP, padrão do Spring Boot)
- Índices e plano de execução (`EXPLAIN PLAN`) — noção básica de performance

**Prática recomendada:**
- Instalar Oracle XE localmente (ou usar Docker) e conectar sua API da Fase 1 a ele
- Adicionar Flyway ao projeto e versionar as alterações de schema

**Critério de avanço:** entender por que uma query está lenta e saber otimizar via índice ou reescrita.

---

## Fase 3 — Testes automatizados: JUnit e Mockito (2 a 3 semanas)

Prática de mercado essencial — projetos sérios (especialmente governamentais, com auditoria) exigem cobertura de testes.

**Tópicos:**
- JUnit 5: `@Test`, `@BeforeEach`, `@ParameterizedTest`, assertions
- Mockito: `@Mock`, `@InjectMocks`, `when/thenReturn`, `verify`
- Testes de unidade vs testes de integração (`@SpringBootTest`, `@DataJpaTest`)
- Testcontainers (muito usado hoje para testar contra Oracle/Redis reais em container, ao invés de mocks/H2)
- Cobertura de código com JaCoCo

**Prática recomendada:**
- Escrever testes para os services e controllers da API que você já construiu
- Meta realista de mercado: 70-80% de cobertura em regras de negócio críticas

**Critério de avanço:** conseguir escrever testes para uma classe nova sem look-up constante de sintaxe.

---

## Fase 3.5 — TDD (Test-Driven Development) (2 a 3 semanas)

Com JUnit e Mockito já dominados como ferramenta, esta fase muda a forma como você escreve código: em vez de codificar e depois testar, você **usa o teste para guiar o design da solução**. É uma mudança de mentalidade, não só de técnica, e costuma ser um diferencial bem visto em processos seletivos mais maduros.

**Tópicos:**
- O ciclo Red-Green-Refactor: escrever o teste que falha, fazer passar com o mínimo de código, depois refatorar com segurança
- Diferença entre TDD clássico (Detroit school, foco em estado) e TDD mockista (London school, foco em interações/mocks) — no seu contexto com Mockito, a abordagem London aparece bastante
- Como o TDD influencia o design: classes mais coesas, menor acoplamento, interfaces mais claras (conecta diretamente com o que você viu em Clean Code/SOLID na Fase 1.5)
- Testes como documentação viva do comportamento esperado do sistema
- Armadilhas comuns: testar detalhes de implementação em vez de comportamento, testes frágeis que quebram a cada refatoração, "TDD teatral" (escrever o teste depois e fingir que veio antes)
- TDD aplicado a APIs REST: como testar um endpoint do zero, do teste de unidade do service até o teste de integração do controller

**Prática recomendada:**
- Pegar uma funcionalidade nova (ainda não implementada) do seu projeto e desenvolvê-la **inteiramente via TDD**: primeiro o teste, depois o código mínimo, depois o refactor
- Comparar a experiência com o jeito "código primeiro, teste depois" que você já praticou na Fase 3 — vale documentar essa reflexão, é um ótimo ponto para falar em entrevista

**Recursos comuns no mercado:**
- Livro: *Test Driven Development: By Example* (Kent Beck) — a referência original do tema
- Livro: *Growing Object-Oriented Software, Guided by Tests* (Freeman & Pryce) — mais avançado, foca na escola "mockista", bem alinhado ao uso de Mockito
- Katas de TDD (ex: "FizzBuzz Kata", "Bowling Game Kata") são exercícios curtos e clássicos para treinar o ciclo Red-Green-Refactor sem a complexidade de um projeto real

**Critério de avanço:** conseguir desenvolver uma funcionalidade pequena do início ao fim seguindo o ciclo Red-Green-Refactor, sem "trapacear" escrevendo o código de produção antes do teste.

---

## Fase 3.75 — Qualidade de Código e CI/CD (2 a 3 semanas)

Até aqui você já escreve código limpo (Fase 1.5) e testado (Fases 3 e 3.5). Agora é hora de **automatizar a verificação dessa qualidade** e o processo de entrega — prática padrão em qualquer empresa de tecnologia madura, e praticamente obrigatória em projetos governamentais por causa de exigências de auditoria e rastreabilidade.

**Tópicos:**
- **Linting:** Checkstyle e/ou PMD para Java (padronização de estilo, detecção de más práticas); ESLint para TypeScript/Angular. Configuração de regras e integração com o editor (fail-fast antes mesmo do commit)
- **SonarQube/SonarCloud:** análise estática de código — bugs, vulnerabilidades, code smells, duplicação; conceito de "Quality Gate" (critério mínimo que o código precisa atingir para ser aprovado); métricas comuns: cobertura de testes, complexidade ciclomática, débito técnico
- **Git hooks:** pre-commit (rodar lint/testes antes do commit) com ferramentas como Husky (mais comum no mundo frontend/Angular) ou hooks nativos do Git
- **CI (Integração Contínua):** pipelines automatizados que rodam build, testes e análise estática a cada push/PR — GitHub Actions, GitLab CI ou Jenkins (este último ainda muito comum em empresas com infraestrutura mais tradicional/on-premise, como costuma ser o caso de sistemas governamentais)
- **CD (Entrega/Implantação Contínua):** conceito de pipeline de deploy (build → testes → análise → deploy em homologação → aprovação → produção); diferença entre Continuous Delivery (deploy manual final) e Continuous Deployment (deploy automático)
- Versionamento semântico (SemVer) e estratégias de branch alinhadas a CI/CD (trunk-based development costuma combinar bem com pipelines rápidos)

**Prática recomendada:**
- Configurar SonarCloud (versão gratuita para projetos públicos) no seu repositório e corrigir os principais alertas apontados
- Criar um pipeline no GitHub Actions que, a cada push: compila o projeto, roda os testes JUnit, roda a análise do Sonar e falha o build se o Quality Gate não passar
- Adicionar um pre-commit hook simples que roda o linter antes de permitir o commit

**Recursos comuns no mercado:**
- Documentação oficial: [docs.sonarsource.com](https://docs.sonarsource.com) e [docs.github.com/actions](https://docs.github.com/actions)
- Muitas empresas usam variações do mesmo conceito com Jenkins/GitLab CI — vale entender o **conceito de pipeline** de forma agnóstica à ferramenta, já que a lógica se transfere facilmente entre elas

**Critério de avanço:** ter um pipeline funcional que barra automaticamente um PR com testes quebrados ou Quality Gate reprovado — sem intervenção manual.

---

## Fase 4 — Redis (2 semanas)

**Tópicos:**
- Conceitos: cache-aside pattern, TTL, invalidação de cache
- Spring Cache abstraction: `@Cacheable`, `@CacheEvict`, `@CachePut`
- Estruturas de dados do Redis (strings, hashes, lists, sets) e quando usar cada uma
- Casos de uso comuns: cache de consultas pesadas, sessões, rate limiting

**Prática recomendada:**
- Adicionar cache na API existente (ex: cachear resultado de uma consulta que hoje é lenta no Oracle)
- Medir e comparar tempo de resposta com e sem cache

---

## Fase 5 — IBM MQ e mensageria (2 a 3 semanas)

**Tópicos:**
- Conceitos de mensageria assíncrona: filas, tópicos, produtores/consumidores
- Spring JMS com IBM MQ: `@JmsListener`, `JmsTemplate`
- Padrões comuns: dead-letter queue, retry, idempotência de consumidores
- Quando usar mensageria vs chamada síncrona (decisão arquitetural que você já vê na prática como analista)

**Prática recomendada:**
- Simular um fluxo assíncrono: um serviço publica uma mensagem (ex: "solicitação criada") e outro serviço consome e processa
- IBM oferece imagem Docker do MQ para testes locais

**Observação:** essa é a tecnologia mais "de nicho" da lista — vale entender bem os conceitos de mensageria de forma geral (também aplicáveis a Kafka/RabbitMQ, mais comuns no mercado amplo), já que IBM MQ especificamente é mais raro fora de ambientes corporativos/legados.

---

## Fase 6 — Angular (Frontend) (6 a 8 semanas, pode rodar em paralelo com Fase 2-5)

**Tópicos:**
- TypeScript básico (tipos, interfaces, decorators)
- Componentes, templates, data binding (`[]`, `()`, `[()]`)
- Services e Injeção de Dependência
- Roteamento (`RouterModule`)
- Consumo de API REST com `HttpClient`
- Reactive Forms (padrão de mercado, mais robusto que Template-driven Forms)
- RxJS básico: `Observable`, `map`, `switchMap`, `subscribe`
- Gerenciamento de estado (para projetos maiores: NgRx — vale ao menos conhecer o conceito)

**Prática recomendada:**
- Construir a tela que consome a API da Fase 1: listagem, formulário de criação/edição, tratamento de erros

**Recursos comuns no mercado:**
- Documentação oficial: [angular.dev](https://angular.dev)
- Curso: Angular da Loiane Groner (referência forte em pt-BR)

---

## Fase 7 — Arquitetura de Microsserviços (3 a 4 semanas)

Com backend, frontend, banco, cache, mensageria e boas práticas de código já consolidados, este é o momento de entender como tudo isso se organiza em escala — muito relevante em empresas que desenvolvem aplicações governamentais, onde sistemas grandes costumam ser decompostos em serviços menores e independentes.

**Tópicos:**
- Monólito vs microsserviços: quando vale a pena migrar (e quando **não** vale — isso é tão importante quanto saber implementar)
- Decomposição por domínio (Domain-Driven Design básico: bounded contexts, agregados)
- Comunicação entre serviços: síncrona (REST, gRPC) vs assíncrona (aqui entra o IBM MQ/mensageria da Fase 5, agora como peça de integração entre serviços)
- API Gateway (Spring Cloud Gateway) e Service Discovery (Eureka) — padrões clássicos do ecossistema Spring Cloud
- Configuração centralizada (Spring Cloud Config)
- Resiliência: Circuit Breaker (Resilience4j), timeout, retry, fallback
- Observabilidade: logs centralizados, tracing distribuído (ex: Zipkin/Sleuth), métricas (Micrometer + Prometheus/Grafana)
- Desafios reais de microsserviços: consistência eventual, transações distribuídas (Saga pattern), versionamento de contratos de API
- Containers e orquestração: Docker (empacotar cada serviço) e noção introdutória de Kubernetes (não precisa dominar, mas é comum aparecer em vagas)

**Prática recomendada:**
- Pegar o monólito construído nas fases anteriores e quebrar em pelo menos 2 serviços independentes (ex: serviço de "solicitações" e serviço de "notificações", comunicando-se via fila)
- Subir os serviços com Docker Compose, incluindo Oracle, Redis e a fila como containers
- Adicionar um API Gateway simples na frente dos dois serviços

**Recursos comuns no mercado:**
- Livro: *Building Microservices* (Sam Newman) — referência de mercado, mesmo sem foco específico em Java
- Documentação: [spring.io/projects/spring-cloud](https://spring.io/projects/spring-cloud)
- Curso: trilhas de "Spring Cloud Microservices" (Udemy/Alura) costumam cobrir Gateway, Eureka e Resilience4j de forma prática

**Observação importante:** microsserviços resolvem problemas de escala e times grandes, mas adicionam complexidade operacional real. Em entrevistas, saber explicar **os trade-offs** (não só a implementação) costuma impressionar mais do que saber configurar Eureka de cor.

**Critério de avanço:** conseguir explicar, com argumentos técnicos, quando você recomendaria microsserviços versus manter um monólito bem estruturado — e ter ao menos dois serviços simples se comunicando de verdade.

---

## Fase 8 — Projeto integrador final (4 a 6 semanas)

Construa **um sistema completo, do zero**, integrando tudo:

**Sugestão de projeto:** um sistema de gestão de solicitações/chamados (aproveitando seu conhecimento de domínio de requisitos), já pensado como **dois ou mais microsserviços**:
- Serviço de "solicitações": Spring Boot com Oracle + Flyway, código estruturado seguindo os princípios de Clean Code/SOLID da Fase 1.5
- Serviço de "notificações": consome mensagens de fila (IBM MQ ou RabbitMQ) e processa de forma assíncrona
- Cache de consultas com Redis no serviço principal
- Comunicação entre os serviços via fila (assíncrona) e/ou REST (síncrona), com resiliência básica (timeout/retry)
- Cobertura de testes com JUnit/Mockito em ambos os serviços, com ao menos uma funcionalidade nova desenvolvida via TDD do início ao fim
- Frontend Angular consumindo a API (via um API Gateway simples, se quiser ir além)
- Containers com Docker Compose subindo tudo junto (serviços + Oracle + Redis + fila)
- Tudo versionado no Git com histórico de commits organizado e README explicando arquitetura e decisões (inclusive por que optou por microsserviços ali, e não monólito)
- Pipeline de CI/CD configurado (ex: GitHub Actions) rodando build, testes e análise do SonarCloud a cada push, com Quality Gate ativo

Esse projeto vira **seu portfólio** — é o que você mostra em entrevistas e no LinkedIn/GitHub.

---

## Dicas práticas para a transição de carreira

1. **Fale sobre isso no trabalho.** Muitas empresas de tecnologia (especialmente as que trabalham com governo) valorizam analista que quer migrar para dev — pode haver espaço para squad rotation ou pair programming com a equipe de desenvolvimento do seu próprio projeto.
2. **Use seu conhecimento de negócio como diferencial.** Um dev que já entende requisitos, regras de negócio complexas e o "porquê" das telas é mais raro e valioso que um dev júnior comum.
3. **Documente sua jornada no GitHub.** Commits frequentes com mensagens claras mostram evolução real para quem for avaliar seu perfil.
4. **Não pule a Fase 0.** É tentador ir direto para Spring Boot, mas fundamentos fracos em Java geram dívida técnica de aprendizado que atrapalha tudo depois.
5. **Participe de code review.** Peça para revisar (ou ser revisado) pelo time de dev do seu projeto atual — é aprendizado prático gratuito e visível.

---

## Cronograma resumido

| Fase | Tecnologia | Duração |
|---|---|---|
| 0 | Java + Git | 3-4 semanas |
| 1 | Spring Boot | 6-8 semanas |
| 1.5 | Clean Code e Boas Práticas | 2-3 semanas |
| 2 | Oracle + JPA | 3-4 semanas |
| 3 | JUnit + Mockito | 2-3 semanas |
| 3.5 | TDD | 2-3 semanas |
| 3.75 | Sonar, Lint e CI/CD | 2-3 semanas |
| 4 | Redis | 2 semanas |
| 5 | IBM MQ | 2-3 semanas |
| 6 | Angular | 6-8 semanas (paralelo) |
| 7 | Arquitetura de Microsserviços | 3-4 semanas |
| 8 | Projeto integrador | 4-6 semanas |

**Total:** aproximadamente 8 a 11 meses, dependendo do ritmo e da possibilidade de paralelizar o frontend com o backend.
