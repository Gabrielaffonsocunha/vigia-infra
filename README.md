# Vigia Infra

Laboratório de observabilidade para infraestrutura com Prometheus, Grafana, Blackbox Exporter e Docker Compose. Reúne sondagem HTTP, métricas do host, dashboard provisionado, alertas e CI de validação.

## Recursos
- Disponibilidade e latência de endpoints HTTP com Blackbox Exporter.
- Métricas de CPU, memória, disco e rede pelo Node Exporter.
- Dashboard Grafana provisionado automaticamente.
- Alertas para endpoint indisponível, latência alta e falha de coleta.
- GitHub Actions valida Compose, Prometheus, regras e JSON.
- Runbook de triagem em `docs/runbook.md`.

## Executar
Requisitos: Docker Engine, Compose v2 e acesso à internet.

1. Clone o repositório e entre na pasta.
2. Copie `.env.example` para `.env` e configure uma senha forte.
3. Execute `docker compose up -d`.
4. Acesse Grafana em http://localhost:3000 (admin e senha do `.env`), Prometheus em http://localhost:9090.

As portas ficam vinculadas a 127.0.0.1. Alvos HTTP de exemplo ficam em `prometheus/prometheus.yml`; substitua por serviços que você tem autorização para monitorar.

## Segurança e escopo
Projeto de laboratório. Não publique `.env` nem use a senha de exemplo em produção. Dados ficam em volumes Docker locais; `docker compose down -v` apaga os dados persistidos. Node Exporter lê métricas do host e seu mount é somente leitura. HA, TLS, backup e notificações externas ficam para evoluções futuras.

## Autor
Gabriel Afonso — Infraestrutura de TI, observabilidade e automação.
