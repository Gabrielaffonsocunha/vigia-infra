# Runbook de triagem

## 1. Confirmar o alerta
1. Abra o Grafana e compare disponibilidade e latência.
2. No Prometheus, consulte `probe_success`, `probe_duration_seconds` e `up`.
3. Verifique se um ou vários endpoints foram afetados e anote o horário.

## 2. Investigar a sondagem HTTP
Consulte `http://localhost:9115/probe?target=https://github.com&module=http_2xx` e examine `probe_success`, status HTTP e erros.
- Um único alvo falha: conferir URL, DNS, certificado e serviço.
- Vários alvos falham: conferir conectividade externa, DNS e host do laboratório.
- Latência alta: comparar duração e período antes de identificar a causa.

## 3. Verificar coleta do host
Execute `docker compose ps` e `docker compose logs --tail=100 node-exporter`. Verifique `up{job="node-exporter"}` no Prometheus. No Docker Desktop, as métricas podem representar a VM Linux.

## 4. Recuperar e registrar
Após corrigir a causa, reinicie somente o serviço afetado com `docker compose restart <serviço>` e confirme a recuperação no Prometheus. Registre impacto, evidências, ação e resultado. Evite `docker compose down -v`, pois ele apaga o histórico persistido.
