# Sistema de Processamento e Publicação de Dados MERGE – Projeto ENANDES

**Projeto ENANDES:** Monitoramento de secas para agricultura e gestão de recursos hídricos usando produtos via satélite  
**Instituto Nacional de Pesquisas Espaciais – INPE**  
São José dos Campos – SP, Brasil  
Agosto de 2025

---

## 1. Objetivo
Esta nota técnica descreve o sistema **enandes-processing**, módulo backend do Projeto ENANDES.

---

## 2. Introdução
O sistema **enandes-processing** foi desenvolvido para automatizar o **processamento**, **conversão**, **indexação** e **publicação** de dados climáticos do produto **MERGE** (Multi-satellitE Retrievals for GPM – CPTEC/INPE) no formato **GeoTIFF**, com suporte a serviços geoespaciais via **GeoServer**.

Principais funcionalidades:
- Integração com **PostGIS**.
- Gerenciamento via **Docker**.
- Conversão de formatos **NetCDF** e **GRIB2** para GeoTIFF.
- Publicação automática de camadas com suporte a tempo.

O **MERGE** (Rozante et al., 2010) é processado no CPTEC/INPE a partir do **IMERGE** (Integrated Multi-satellitE Retrievals for GPM) da NASA, atualmente na versão 7B.
- **Link do produto MERGE:** https://clima.cptec.inpe.br/monitoramentobrasil/pt
- **Link FTP de dados MERGE:** https://ftp.cptec.inpe.br/modelos/tempo/MERGE/GPM/

No contexto do **Projeto ENANDES**, a base é convertida para **GeoTIFF**, cadastrada no GeoServer e disponibilizada via serviços **WMS** em:
[https://satelite.cptec.inpe.br/enandes/](https://satelite.cptec.inpe.br/enandes/)

---

## 3. Arquitetura do Sistema
O sistema é baseado em **scripts Python** organizados para:

- Baixar dados MERGE via HTTP  
  `https://ftp.cptec.inpe.br/modelos/tempo/MERGE/GPM/...`;
- Converter **NetCDF** e **GRIB2** para **GeoTIFF**;
- Popular base de dados **PostGIS** (`merge_index`);
- Publicar no **GeoServer** via camada **ImageMosaic** com suporte a tempo;
- Aplicar estilos **SLD** para visualização.

**Estrutura de diretórios:**

$HOME/enandes-processing

- ├── batch # Scripts de processamento e publicação;
- ├── config # Arquivos de configuração JSON;
- ├── downloaders # Módulos de download (MERGE, SPI, SPEI etc.);
- ├── utils # Funções auxiliares;
