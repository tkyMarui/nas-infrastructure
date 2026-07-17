# NAS Infrastructure

Infraestrutura robusta de armazenamento em rede com redundância, backup automatizado, acesso remoto seguro e monitoramento de tráfego.

## Objetivos

Construir uma pequena simulação de uma infraestrutura empresarial que cobre : cloud privada para os funcionários, armazenamento dedicado a redundância + velocidade, backups periódicos e acesso remoto seguro

Este projeto consiste em dois servidores Linux dedicados:

- **Servidor principal NAS**: Xubuntu, 8 GB de RAM, 4 núcleos
  - 4 discos storage em **RAID 10**
  - 1 disco configurado como **hot spare**
- **Servidor de backup**: Ubuntu Server, 8 GB de RAM, 4 núcleos
  - 5 discos storage em **RAID 6**
  - 1 disco configurado como **hot spare**

## Features implementadas

- Nextcloud + MySQL em Docker Compose
- Volume do Nextcloud montado dentro da RAID 10
- Snapshots com Back In Time para as pastas dos setores
- Backup sincronizado por `rsync` com chaves de acesso
- Backup agendado diariamente com `cron`  
- Acesso remoto ao Nextcloud com VPN Tailscale
- Filtragem, bloqueio de anúncios e análise de tráfego com Pi-hole em Docker Compose
- Firewall com UFW (deny incoming por padrão + liberação explícita de serviços essenciais)

## Este projeto demonstra competências práticas em:

- planejamento de infraestrutura
- implementação de armazenamento com RAID para tolerância a falhas e melhor desempenho de acesso aos dados
- automação de backup
- administração Linux
- organização de serviços em containers
- acesso remoto seguro
- separação entre dados primários e cópias de segurança

Além de construir um ambiente funcional e documentado, o projeto demonstra preocupação com desempenho, disponibilidade dos serviços e continuidade operacional, utilizando redundância de armazenamento, snapshots e um servidor de backup dedicado.

## Resultado esperado

- Servidor NAS central para armazenamento e compartilhamento, e Backup fisicamente isolado
- Acesso remoto sem exposição direta de portas na internet
- Redução de risco de perda de dados
- Base sólida para evoluções futuras

## Conhecimentos Demonstrados

✅ Infraestrutura e Storage  
✅ Redes (RAID, LVM, NFS, SMB)  
✅ Segurança (Firewall, VPN, DNS filtering)  
✅ Containerização (Docker)  
✅ Backup e Disaster Recovery    
✅ Automação (scripts, cron jobs)  
✅ Troubleshooting  
✅ Hardening de SSH (acesso por chaves) 

## 🚀 Updates futuros

- (hipotético) Implementar VPN WireGuard - competências já presentes, porém, não aplicado, pois não havia necessidade pagar uma VPS apenas para a simulação
- Monitoramento com Prometheus
- Sistema de alertas (e-mail) para falhas de RAID, backup e serviços
- Implementação de Fail2Ban para proteção contra tentativas de brute force
- Logs centralizados e análise de eventos

**Última atualização:** 05/03/26
