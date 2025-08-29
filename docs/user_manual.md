

---

## Manual Geral do Usuário

### Acessar a máquina DIADEMA
``` Via ssh e linha de comando bash;
cd /scripts/enandes/enandes-processing

### Instalação
cd /scripts/enandes

Utilizar o grupo `enandes` com sudo;
Link clone: https://github.com/dissm-inpe/enandes-processing.git

Ou para Atualização (grupo `enandes`);
cd /scripts/enandes/enandes-processing;
git fetch;
git pull; 


### Configuração

Editar config/config_enandes_production.json para definir:

    Diretórios de entrada/saída

    Ambiente Python

### Ativar ambiente Python

conda activate env-enandes-processing

### Execução dos Produtos

Modo Operacional (processa data atual):
--start_date "" --end_date ""

Modo Período (intervalo específico):
--start_date "YYYYMMDD" --end_date "YYYYMMDD"

### Exemplos:

MERGE-DAILY  (Processa diariamente) 

nohup python3 batch/operacional_process_merge_daily.py \
  --config "config/config_enandes_production.json" \
  --start_date "" --end_date ""

[![Fluxo do processo MERGE Daily]](d01_merge_daily.png)


MERGE-HOURLY  (Processa diariamente)

nohup python3 batch/operacional_process_merge_hourly.py \
  --config "config/config_enandes_production.json" \
  --start_date "" --end_date ""

[![Fluxo do processo MERGE Hourly]](d02_merge_hourly.png)

MERGE-SPI  (Processa memsalmente, especificamente no dia 02)

~/enandes-processing$ python3 batch/operacional_process_merge_SPIeSPEI.py \
--config "config/config_enandes_test.json" \
--start_date "20250822" --end_date "20250822"


Download - DAILY

python3 enandes_processing/downloaders/merge_download.py \
-i https://ftp.cptec.inpe.br/modelos/tempo/MERGE/GPM/DAILY/ \
-o /home/jurandir/data_enandes/tempo/MERGE/GPM/ \
-b 2010-01-01 -e 2010-01-05

Download - SPI

python3 enandes_processing/downloaders/climatology.py **(\**)
-i https://ftp.cptec.inpe.br/modelos/tempo/MERGE/GPM/SPI **(\**)
-o /home/jurandir/data_enandes/tempo/MERGE/GPM/SPI **(\**)
-b 2024-01-01 -e 2024-12-31  --mode spi


###CLIMATOLOGY### 

CLIMATOLOGY DAILY AVERAGE

python3 batch/operacional_process_merge_climatology_daily.py 
--config config/config_enandes_test.json  --start_date 20240101 
--end_date 20241231



CLIMATOLOGY MONTHLY ACCUMULATED  e  CLIMATOLOGY MONTHLY AVERAGE

python3 batch/operacional_process_merge_climatology_monthly.py 
--config config/config_enandes_test.json  --start_date 20240101 
--end_date 20241231



CLIMATOLOGY MONTHLY ACCUMULATED YEARLY  e  CLIMATOLOGY MONTHLY AVERAGE YEARLY

python3 batch/operacional_process_merge_climatology_monthly_yearly.py 
--config config/config_enandes_test.json  --start_date 19980101 
--end_date 20251231



YEAR ACCUMULATED

python3 batch/operacional_process_merge_climatology_year_acc.py 
--config "config/config_enandes_production.json"  --start_date "19980101" 
--end_date "20251231"


###Produtos Suportados###

    MERGE

        DAILY

        HOURLY

    Índices SPI/SPEI

        Gamma

        Pearson

    Climatologias

        DAILY_AVERAGE

        MONTHLY_ACCUMULATED

        MONTHLY_ACCUMULATED_YEARLY

        MONTHLY_AVERAGE

        MONTHLY_AVERAGE_YEARLY

        YEAR_ACCUMULATED

    Déficit Hídrico

        CDD

        MCWD

        MCWD_AN

        AMCWD (Não está no GeoServer mas está na base de dados).


###Observações###

    Processos anuais ou de longo prazo podem ser agendados via crontab para evitar ociosidade.

    O estilo SLD deve estar corretamente configurado para exibição adequada das camadas.

