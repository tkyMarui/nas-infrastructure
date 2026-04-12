# 🔐 Modelo de Segurança em Camadas

## Camada 1: Perímetro
- Firewall (sistema Linux / roteador)
- Port filtering
- Sem exposição direta de serviços na internet

## Camada 2: Acesso
- Pi-hole (DNS filtering e bloqueio de domínios)
- Tailscale VPN (acesso remoto privado)
- Autenticação de usuário (Nextcloud)

## Camada 3: Transporte
- HTTPS (Nextcloud)
- VPN criptografada (Tailscale / WireGuard)
- Comunicação interna protegida via rede privada Tailscale

# 📊 RTO/RPO (Recovery Time / Point Objectives)
| Cenário | RTO | RPO | Impacto |
|---------|-----|-----|---------|
| Falha de 1 disco (NAS - RAID 10) | 30 min – 2 h | ~0 min | Mínimo |
| Falha de 1 disco (Backup - RAID 6) | 1 – 4 h | ~0 min | Baixo |
| Falha completa do NAS | 4 – 24 h | até 24 h | Moderado |
| Corrupção de dados | 30 min – 2 h | minutos – horas | Baixo |
| Exclusão acidental | minutos | minutos – horas | Baixo |
| Perda total do servidor principal | 6 – 24 h | até 24 h | Alto |

# 🔄 Matriz de Falhas e Resiliência
| Cenário de Falha | Probabilidade | Impacto | Mitigação |
|------------------|---------------|---------|-----------|
| Falha de 1 disco (NAS) | Média | Baixo | RAID 10 + hot spare |
| Falha de 1 disco (backup) | Média | Baixo | RAID 6 |
| Falha de múltiplos discos (backup) | Baixa | Médio | RAID 6 (limite de tolerância) |
| Falha total do NAS | Baixa | Alto | Backup em servidor separado |
| Corrupção de dados | Média | Alto | Snapshots + backup |
| Exclusão acidental | Alta | Médio | Back In Time |
| Falha de rede | Baixa | Baixo | Tailscale |
| Falha de energia | Baixa | Médio | Reboot + rebuild RAID |
# 📈 Métricas de Performance

### Leitura
- RAID 10: ~400–600 MB/s (paralelismo)
- Samba/Nextcloud: ~80–150 MB/s (limitado por rede)
- Tailscale: depende da latência (~10–50 MB/s típico remoto)

### Escrita
- RAID 10: ~200–400 MB/s
- Nextcloud: ~30–80 MB/s (overhead de aplicação + DB)
- Backup (rsync): variável conforme delta de dados

# 🌡️ Monitoramento de Saúde

- RAID Status: `cat /proc/mdstat`
- Detalhes RAID: `mdadm --detail /dev/md0`
- Uso de Disco: `df -h`
- SMART: smartctl `-a /dev/sdX`
- Memória: `free -h`
- CPU: `htop`
- Containers: `docker ps` / `docker stats`
