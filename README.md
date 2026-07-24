
# Cauã De Martin

Desenvolvedor backend Python/Django. Trabalho hoje em duas frentes que parecem distantes — logística internacional e análise de movimento por visão computacional — e cobram a mesma coisa: sistema em produção, com usuário real, dado que não pode vazar e entrada que eu não controlo. Django sério de um lado, algoritmo e processamento de sinal do outro.

## O que eu construo

**Logística internacional / comércio exterior.** Plataforma multi-tenant de rastreamento de cargas. O problema aqui é domínio: logística marítima, containerização, Incoterms, deadlines portuários, documentação de exportação e validação fiscal brasileira (CNPJ, CEP, inscrição estadual) — regra demais para caber em CRUD. Construí os wizards de documentação (multi-step, dezenas de inline formsets, validação em cascata, persistência transacional), o isolamento por empresa em toda a camada de models/views/forms e os pipelines de scraping resiliente das fontes externas que antes eram planilha.

**Análise de movimento por visão computacional.** O aluno grava a série no celular, o app extrai os keypoints com YOLO Pose on-device e o servidor compara a execução contra um template de referência para dizer quantas repetições saíram e quão bem foram feitas. Toco o backend dessa frente — Django + DRF com ~170 rotas em 10 módulos, JWT com Argon2, OpenAPI gerado do código, Celery + Redis para o processamento pesado, Postgres/RDS, S3, deploy em Docker — e escrevi o pipeline de segmentação e comparação, que é onde mora a dificuldade real do produto.

## O que eu faço bem

- **Isolamento de dados como decisão de arquitetura** — multi-tenancy por empresa via managers customizados e mixins de formulário, aplicada de forma consistente em models, views e forms, com permissão granular separando quem vê dado operacional de quem vê relatório analítico. Do outro lado, consolidei o consentimento de compartilhamento de mídia em um único gate: vídeo, keypoints e esqueleto passam pelo mesmo porteiro, com snapshot de auditoria por upload. Três caminhos com três regras diferentes é como um vazamento acontece.
- **Algoritmo, não só CRUD** — segmentação de repetições com Savitzky-Golay e detecção bidirecional de picos e vales (tripla vale-pico-vale), DTW sobre features angulares em vez de coordenadas cruas, calibração dos parâmetros do detector por grid search por template. Quando o log de produção dizia 6 repetições e o vídeo tinha 16, rotulei os 14 vídeos à mão, achei a causa (vales sintéticos descartados + janela mínima fixa entre picos) e derrubei o erro médio de 5,1 para 1,3 repetições.
- **Isolamento de processos pesados** — worker de scraping em container próprio para que um OOM não derrube a API; container do Celery em crash-loop silencioso (exit 137, zero traceback) porque o boot importava Ultralytics.
- **Depuração até a raiz, com medição** — homologação consumindo a fila de produção porque compartilhava o DB 0 do Redis; teste flaky de N+1 que contava as queries do próprio profiler. Nada disso aparece no stack trace; aparece quando você mede.
- **Dinheiro e integração que não podem falhar em silêncio** — Stripe Connect com destination charges, onboarding de conta conectada 100% via API, webhooks verificados em produção e reconciliação como backstop idempotente.
- **Teste que exercita o sistema real** — ~240 arquivos com pytest e factory-boy, incluindo suíte contra Postgres de verdade quando o SQLite mente sobre o comportamento do banco. Rodei o fluxo de pagamento end-to-end com chave de teste real e peguei três defeitos que o mock do gateway escondia.

## Stack

**Backend** — Python · Django 4.2 · DRF · FormTools (wizards) · Crispy Forms · Celery · Redis · APScheduler · JWT/Argon2 · drf-spectacular · Stripe · django-money · django-storages · pytest · factory-boy

**Dados** — PostgreSQL/RDS (pg_trgm, índices GIN, full-text search) · modelagem relacional complexa · migrations versionadas · Decimal para valor financeiro

**Infra** — Docker · docker-compose · AWS (EC2, ECS, RDS, S3, Lambda, Secrets Manager) · Serverless Framework · Nginx · Whitenoise · Grafana · deploy multi-ambiente

**Sinal e visão** — NumPy · SciPy · OpenCV · YOLO Pose (Ultralytics) · DTW · Savitzky-Golay · grid search de parâmetros

**Automação** — Playwright · Camoufox · BeautifulSoup · pipelines de coleta resilientes

**Frontend** — Django Templates · Bootstrap 5 · progressive enhancement no estilo HTMX · JS vanilla

## Como eu trabalho

- Bug reportado é sintoma. Antes de editar, procuro todos os chamadores da função e conserto no ponto por onde todos passam.
- Mudança de contrato (rota, serializer, formato de resposta) só sobe depois de cobrir os casos de borda.
- Documento decisão, não código: o porquê de cada escolha, o que foi refutado e o que ficou pendente.
- Prefiro apagar código a adicionar. Abstração que existe para um caso só é dívida com aparência de arquitetura.

Clean Code, Clean Architecture, SOLID e Object Calisthenics como referência e não como religião: camada de serviços separada de views e models, domínio em pt-BR e código em inglês.

## Certificações

- **[Ultralytics YOLO in Production](https://academy.ultralytics.com/courses/yolo-in-production/certificate/fa3abed9-5d4a-404e-b193-0d2ae9283142)** — Ultralytics Academy · Jul/2026 · score 100% · verificado

## Contato

cauademartin@gmail.com
