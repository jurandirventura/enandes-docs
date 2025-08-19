## Fluxo Geral do Sistema – enandes-processing

O fluxo a seguir representa a execução dos principais scripts localizados em  
`/home/jurandir/enandes-processing/batch/`  
Todos seguem o mesmo padrão geral: download, conversão para GeoTIFF, indexação no PostGIS e publicação no GeoServer.

```mermaid
flowchart TD
    A[Início] --> B{Selecionar produto a processar}

    %% Caminhos de escolha
    B --> C1[MERGE-DAILY\noperacional_process_merge_daily.py]
    B --> C2[MERGE-HOURLY\noperacional_process_merge_hourly.py]
    B --> C3[Climatologia Diária\noperacional_process_merge_climatology_daily.py]
    B --> C4[Climatologia Mensal\noperacional_process_merge_climatology_monthly.py]
    B --> C5[Climatologia Mensal Acumulada Ano\noperacional_process_merge_climatology_monthly_yearly.py]
    B --> C6[Climatologia Anual Acumulada\noperacional_process_merge_climatology_year_acc.py]
    B --> C7[SPI/SPEI\noperacional_process_merge_SPIeSPEI.py]
    B --> C8[Processamento Geral\noperacional_process_merge.py]

    %% Passos comuns a todos os scripts
    C1 --> D[Download do produto via módulo downloader]
    C2 --> D
    C3 --> D
    C4 --> D
    C5 --> D
    C6 --> D
    C7 --> D
    C8 --> D

    D --> E[Conversão para GeoTIFF\n(chamada de merge2tif.py quando aplicável)]
    E --> F[Atualização da base PostGIS\n(merge_index)]
    F --> G[Publicação no GeoServer\nvia ImageMosaic]
    G --> H[Aplicação do estilo SLD específico]
    H --> I[Fim]

