

---

## Manual do Usuário

### 1. Acessar a máquina DIADEMA
```bash
cd /scripts/enandes/enandes-processing

2. Configuração

Editar config/config_enandes_production.json para definir:

    Diretórios de entrada/saída

    Ambiente Python

3. Ativar ambiente Python
conda activate env-enandes-processing

4. Execução dos Produtos
Modo Operacional (processa data atual)
--start_date "" --end_date ""

Modo Período (intervalo específico)
--start_date "YYYYMMDD" --end_date "YYYYMMDD"

Exemplos:

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
python3 enandes_processing/downloaders/climatology.py \
-i https://ftp.cptec.inpe.br/modelos/tempo/MERGE/GPM/SPI \
-o /home/jurandir/data_enandes/tempo/MERGE/GPM/SPI \
-b 2024-01-01 -e 2024-12-31  --mode spi

Produtos Suportados

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

        AMCWD


Observações

    Processos anuais ou de longo prazo podem ser agendados via crontab para evitar ociosidade.

    O estilo SLD deve estar corretamente configurado para exibição adequada das camadas.

