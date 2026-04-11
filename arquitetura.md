# Diagrama detalhado da arquitetura

<img width="1253" height="357" alt="image" src="https://github.com/user-attachments/assets/8aa74b57-181b-4a5d-afdb-0d0761ff0a7f" />

## RAID 10 no servidor principal

Combina espelhamento e striping, oferecendo alta performance e redundância

### Uso:

- leitura e escrita intensivas
- base para o volume do Nextcloud e dados em produção

## RAID 6 no servidor de backup

Maior tolerância a falhas (até 2 discos) com dupla paridade, adequado para retenção de backups

### Uso:

- foco em resiliência, não em velocidade bruta

## Hot spare

Disco reserva que reocupa automaticamente os afetados por falha, iniciando o rebuild imediato e reduzindo o tempo de exposição a novas falhas
