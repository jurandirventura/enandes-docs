# ENANDES Processing

> **Sistema de Processamento e Publicação de Dados MERGE**  
> Projeto ENANDES – Monitoramento de secas para agricultura e gestão de recursos hídricos usando dados via satélite  
> Instituto Nacional de Pesquisas Espaciais – INPE

---

## 📌 Sobre o Projeto
- **Programa Associado:** Projeto BIG;
- **Unidade Responsável:** Coordenação Geral de Ciências da Terra - CGCT;
- **Unidade Executora:** Divisão de Previsão de Tempo e Clima – DIPTC/CGCT,
                   Divisão de Satélites e Sensores Meteorológicos - DISSM/CGCT,
                   Divisão de Observação da Terra e Geoinformática. - DIOTG/CGCT;
- **Objeto do Projeto:** Monitoramento da evolução de secas na agricultura e na gestão de recursos hídricos
                   usando produtos gerados a partir de satélites ambientais para os países do consorcio
                   ENANDES (Melhoria da Capacidade de Adaptação das Comunidades Andinas através
                   dos Serviços Climáticos).


## 📌 Sobre o Sistema

O **enandes-processing** é um sistema backend desenvolvido em **Python** para automatizar:

- **Download** dos dados MERGE (CPTEC/INPE);
- **Conversão** dos formatos NetCDF e GRIB2 para GeoTIFF;
- **Indexação** no banco de dados **PostGIS**;
- **Publicação** via **GeoServer** (ImageMosaic com suporte a tempo);
- **Aplicação** de estilos **SLD** para visualização.

O sistema foi projetado para uso no contexto do **Projeto ENANDES**, apoiado pelo Banco Mundial, visando a gestão hídrica e agricultura sustentável na América do Sul.

---

## 🗂 Estrutura da Documentação

| Seção | Descrição |
|-------|-----------|
| [Introdução](introduction.md) | Contexto e objetivos do sistema |
| [Tecnologias Utilizadas](technology_used.md) | Ferramentas, bibliotecas e formatos |
| [Entrada e Saída](input_output.md) | Estrutura dos dados de entrada e saída |
| [Publicação no GeoServer](publish_geoserver.md) | Processo de disponibilização das camadas |
| [Manual do Usuário](user_manual.md) | Passos para instalação e operação |
| [Fluxo Geral](fluxo_geral.md) | Visão completa da arquitetura |
---

## 🚀 Acesso Rápido

- 🌐 **Visualização online:** [ENANDES WebMap](https://satelite.cptec.inpe.br/enandes/)
- 📂 **Código-fonte:** Disponível no repositório do projeto [enandes-processing](https://github.com/dissm-inpe/enandes-processing)

---

"Licença e Reutilização"
    O sistema é aberto para uso em projetos relacionados ao ENANDES.

---

## 📅 Histórico
- **Agosto/2025** – Versão atual da documentação baseada em **MkDocs**.

