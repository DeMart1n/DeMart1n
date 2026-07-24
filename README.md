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

---

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white" alt="Django">
  <img src="https://img.shields.io/badge/DRF-A30000?style=flat-square&logo=django&logoColor=white" alt="Django REST Framework">
  <img src="https://img.shields.io/badge/Celery-37814A?style=flat-square&logo=celery&logoColor=white" alt="Celery">
  <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis">
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white" alt="AWS">
  <img src="https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white" alt="Nginx">
  <img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white" alt="Grafana">
  <br>
  <img src="https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/SciPy-8CAAE6?style=flat-square&logo=scipy&logoColor=white" alt="SciPy">
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white" alt="OpenCV">
  <img src="https://img.shields.io/badge/Ultralytics-0B23A9?style=flat-square&logo=ultralytics&logoColor=white" alt="Ultralytics">
  <img src="https://img.shields.io/badge/Stripe-635BFF?style=flat-square&logo=stripe&logoColor=white" alt="Stripe">
  <img src="https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white" alt="Playwright">
  <img src="https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white" alt="pytest">
  <img src="https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white" alt="Bootstrap">
</p>
