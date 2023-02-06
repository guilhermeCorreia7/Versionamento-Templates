Configuração do script de monitoramento do Veeam.
Referência: https://share.zabbix.com/cat-app/backup/veeam-backup-recovery-jobs-trapper

Adicionar estas informações no arquivo de configuração do User_Parameter.conf na pasta "zabbix_agentd.conf.d": 
  > UserParameter=vbr[*],powershell -NoProfile -ExecutionPolicy Bypass -File "C:\Program Files\Zabbix Agent\scripts\zabbix_vbr_job.ps1" "$1" "$2" "$3"
  > 
  > UserParameter=license[*],powershell -NoProfile -ExecutionPolicy Bypass -File "C:\Program Files\Zabbix Agent\scripts\veeam-lic-info.ps1" "$1"
 
Criar a pasta "scripts" em "C:\Program Files\Zabbix Agent\" e adicionar os dois arquivos dentro dessa pasta:
  > zabbix_vbr_job.ps1
  > 
  > veeam-lic-info.ps1

Ajustar o script de configuração do agente, adicionando a permissão para execução dos comandos:
  > AllowKey=system.run[*]
  > 
  > UnsafeUserParameter=1

Abrir o PowerShell como Administrador e executar o comando: 
  > Set-ExecutionPolicy Unrestricted
  > 
  > Colocar a opção "[A]Yes To All"

Feito isso, reiniciar o agente e aguardar tempo de coleta.

No front-end do Zabbix, clonar o template "Template Veeam - Backup and Replication" para o cliente específico e adicionar o template. 

Aguardar o tempo de coleta.
