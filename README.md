# Análise de Acessibilidade Urbana e Teoria dos Grafos (Parte 02)

Este repositório contém o desenvolvimento da **Parte 2** do Trabalho Final da disciplina de **Teoria dos Grafos**. O projeto consiste na modelagem e análise da acessibilidade da malha viária urbana e da distribuição de serviços públicos essenciais em duas cidades catarinenses: **Lauro Müller (SC)** e **Arvoredo (SC)**.

O trabalho utiliza dados espaciais reais do **OpenStreetMap (OSM)** via biblioteca `osmnx` e aplica conceitos clássicos de teoria dos grafos (como componentes conexas e o algoritmo de Dijkstra) para mapear e avaliar o acesso da população a escolas, creches, postos de saúde, hospitais e assistência social (CRAS).

---

## 🎯 Objetivos do Trabalho

1. **Modelagem de Malha Viária como Grafo**:
   * Baixar e limpar a rede viária do perímetro urbano das cidades de Lauro Müller e Arvoredo.
   * Extrair a **maior componente fracamente conectada** de cada rede viária e convertê-las em grafos não-direcionados para garantir consistência nas análises de rotas peatonais.
2. **Partição Territorial**:
   * Organizar os grafos agrupando as vias e conexões por bairros em Lauro Müller (usando subdivisões do OSM).
   * Dividir a malha urbana compacta de Arvoredo em **4 quadrantes** (Setores Noroeste, Nordeste, Sudoeste e Sudeste) para fins comparativos de densidade.
3. **Injeção de Pontos de Interesse**:
   * Definir **3 pontos de referência** em marcos públicos oficiais de cada cidade (Prefeituras, Praças e Portais) para simular origens de trajetos.
   * Georreferenciar e associar a localização de **serviços públicos reais** nos nós mais próximos da rede viária do grafo.
4. **Cálculo de Caminhos Mais Curtos**:
   * Encontrar o caminho de menor custo (em metros nas vias reais) a partir de cada marco de referência até o serviço público mais próximo de cada tipo usando o **Algoritmo de Dijkstra**.
   * Estimar tempos de deslocamento baseados em caminhada (velocidade média de 4.5 km/h).
5. **Análise de Cobertura Espacial (Buffers)**:
   * Determinar quais e quantos serviços estão dentro de raios de **1 km** (caminhada rápida) e **5 km** (transporte motorizado) ao redor dos marcos de referência.
6. **Análise Comparativa de Densidade**:
   * Comparar a distribuição e densidade de serviços públicos entre pelo menos 4 bairros/setores de cada município através de tabelas e gráficos.
7. **Relatórios e Recomendações**:
   * Identificar vazios de atendimento e sugerir coordenadas ideais para a implantação de novos serviços de utilidade pública.

---

## 🛠️ Tecnologias Utilizadas

A solução foi implementada inteiramente em **Python** dentro de um ambiente Jupyter Notebook, utilizando as seguintes bibliotecas:

* **[OSMnx](https://osmnx.readthedocs.io/)**: Para download, simplificação e visualização geométrica de grafos de ruas do OpenStreetMap.
* **[NetworkX](https://networkx.org/)**: Para manipulação das estruturas de dados do grafo e execução do algoritmo de caminho mais curto (Dijkstra).
* **[Folium](https://python-visualization.github.io/folium/)**: Para a geração de mapas interativos em modo escuro premium (*CartoDB Dark Matter*).
* **[Matplotlib](https://matplotlib.org/)**: Para a renderização dos gráficos estáticos de densidade por setor.
* **[Pandas](https://pandas.pydata.org/) & [NumPy](https://numpy.org/)**: Para tratamento de tabelas de dados, pivotamento e cálculos matemáticos.
* **[Shapely](https://shapely.readthedocs.io/) & [GeoPandas](https://geopandas.org/)**: Para tratamento e projeção de geometrias espaciais.

---

## 📂 Estrutura de Arquivos

* 📄 **`trabalho_grafos_parte2.ipynb`**: Notebook Jupyter principal, contendo toda a execução dos códigos comentada, mapas folium incorporados e os relatórios em Markdown.
* 🌐 **`mapa_lauro_caminhos.html`** / **`mapa_arvoredo_caminhos.html`**: Mapas interativos mostrando a malha urbana, os serviços e as rotas ótimas de Dijkstra traçadas em neon.
* 🌐 **`mapa_lauro_cobertura.html`** / **`mapa_arvoredo_cobertura.html`**: Mapas interativos contendo os círculos de alcance de 1 km (linha contínua) e 5 km (linha tracejada) ao redor dos marcos de referência.
* 🖼️ **`mapa_bairros_lauro.png`** / **`mapa_bairros_arvoredo.png`**: Grafos com a malha viária colorida por bairro/setor no tema escuro.
* 🖼️ **`grafico_densidade_servicos.png`**: Gráfico comparativo de distribuição de serviços públicos por setor.

---

## 🚀 Como Rodar o Projeto

### Pré-requisitos
Certifique-se de possuir o Python instalado (recomenda-se a distribuição **Anaconda** para maior facilidade com dependências científicas).

### Passo 1: Configurar o Ambiente e Instalar Dependências
Abra o seu terminal (Prompt do Anaconda ou Terminal do VS Code) na pasta do projeto e instale as bibliotecas necessárias:

```bash
# Caso prefira usar conda (altamente recomendado para geopandas e osmnx):
conda create -n grafos python=3.10 -y
conda activate grafos
conda install -c conda-forge osmnx geopandas networkx matplotlib folium pandas numpy shapely -y

# Caso prefira utilizar o pip convencional:
pip install osmnx geopandas networkx matplotlib folium pandas numpy shapely notebook
```

### Passo 2: Executar o Jupyter Notebook
Inicie o servidor do Jupyter executando:

```bash
jupyter notebook
```

No navegador que se abrir, clique sobre o arquivo **`trabalho_grafos_parte2.ipynb`** e selecione a opção **"Run All"** (ou **"Executar tudo"**) para carregar a malha urbana, reprocessar as rotas de Dijkstra e abrir os mapas interativos.
