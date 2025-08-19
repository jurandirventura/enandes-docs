# Fluxo Geral

```mermaid
flowchart TB
    A[Início]:::start --> B{Selecionar produto a processar}:::decision

    %% Caminhos de escolha
    B --> C1["MERGE-DAILY\noperacional_process_merge_daily.py"]:::process
    B --> C2["MERGE-HOURLY\noperacional_process_merge_hourly.py"]:::process
    B --> C3["Climatologia Diária\noperacional_process_merge_climatology_daily.py"]:::process
    B --> C4["Climatologia Mensal\noperacional_process_merge_climatology_monthly.py"]:::process
    B --> C5["Climatologia Mensal Acumulada Ano\noperacional_process_merge_climatology_monthly_yearly.py"]:::process
    B --> C6["Climatologia Anual Acumulada\noperacional_process_merge_climatology_year_acc.py"]:::process
    B --> C7["SPI/SPEI\noperacional_process_merge_SPIeSPEI.py"]:::process
    B --> C8["Processamento Geral\noperacional_process_merge.py"]:::process

    %% Passos comuns
    C1 --> D["Download do produto via módulo downloader"]:::process
    C2 --> D
    C3 --> D
    C4 --> D
    C5 --> D
    C6 --> D
    C7 --> D
    C8 --> D

    D --> E["Conversão para GeoTIFF\n(merge2tif.py quando aplicável)"]:::process
    E --> F["Atualização da base PostGIS\n(merge_index)"]:::process
    F --> G["Publicação no GeoServer\nvia ImageMosaic"]:::process
    G --> H["Aplicação do estilo SLD específico"]:::process
    H --> I[Fim]:::end

    %% Estilos
    classDef start fill:#4CAF50,stroke:#333,stroke-width:2px,color:#fff;
    classDef decision fill:#FFC107,stroke:#333,stroke-width:2px,color:#000;
    classDef process fill:#03A9F4,stroke:#333,stroke-width:1px,color:#fff;
    classDef end fill:#E91E63,stroke:#333,stroke-width:2px,color:#fff;

```
