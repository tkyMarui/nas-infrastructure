# NAS Infrastructure

Infraestrutura robusta de armazenamento em rede com redundância, backup automatizado, acesso remoto seguro e monitoramento de tráfego.

## Objetivos

Construir uma pequena simulação de uma infraestrutura empresarial que cobre : cloud privada para os funcionários, armazenamento dedicado a redundância + velocidade, backups periódicos, acesso remoto seguro e observabilidade básica.

Este projeto consiste em dois servidores Linux dedicados:

- **Servidor principal NAS**: Xubuntu, 8 GB de RAM, 4 núcleos
  - 4 discos para storage em **RAID 10**
  - 1 disco configurado como **hot spare**
- **Servidor de backup**: Ubuntu Server, 8 GB de RAM, 4 núcleos
  - 5 discos para storage em **RAID 6**
  - 1 disco configurado como **hot spare**

## Features implementadas

- Nextcloud + MySQL em Docker Compose
- Volume do Nextcloud montado dentro da RAID 10
- Snapshots com Back In Time para as pastas dos setores
- Backup sincronizado por `rsync` em `SSH` com chaves de acesso
- Backup agendado diariamente com `cron`  
- Acesso remoto ao Nextcloud com VPN Tailscale (Wireguard)
- Filtragem, bloqueio de anúncios e análise de tráfego com Pi-hole em Docker Compose
- Firewall com UFW (deny incoming por padrão + liberação explícita de serviços essenciais)

## Por que este projeto é importante ?

Este projeto demonstra competências práticas em:

- planejamento de infraestrutura
- tolerância a falhas
- automação de backup
- administração Linux
- organização de serviços em container
- acesso remoto seguro
- separação entre dados primários e cópias de segurança

Ele mostra capacidade de construir um ambiente funcional, documentado e resiliente, com preocupação real com continuidade operacional.

## Resultado esperado

- Servidor NAS central para armazenamento e compartilhamento, e Backup fisicamente isolado
- Acesso remoto sem exposição direta de portas na internet
- Redução de risco de perda de dados
- Base sólida para evolução futura com monitoramento, alertas e hardening

**Última atualização:** 2026-04-11
