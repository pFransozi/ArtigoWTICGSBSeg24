# SBSeg'24 Seleção de Características Multi-objetivo para Detecção de Malwares Android

## Apresentação

Este repositório está atrelado ao artigo "Seleção de Características Multi-objetivo para Detecção de *Malwares* Android". O artigo foi publicado no XVIII Workshop de Trabalhos de Iniciação Científica e de Graduação (WTICG) do 24º Simpósio Brasileiro em Segurança da Informação e de Sistemas Computacionais.

**Título**: Seleção de Características Multi-objetivo para Detecção de Malwares Android.


**Resumo**: Este artigo propõe um modelo de detecção *multi-view* de *Android* implementado em duas etapas. Na primeira etapa, um conjunto de múltiplas características é extraído de pacotes de aplicativos *Android*, fornecendo um vetor comportamental do aplicativo para a tarefa de classificação, aumentando a generalização. A segunda etapa consiste em realizar uma otimização multiobjetivo para selecionar um subconjunto ideal de características baseado em cada *view* para classificação com método *ensemble*. Os experimentos em nosso novo *dataset*, composto por aproximadamente 40 mil amostras de aplicativos, demonstraram a viabilidade de nossa proposta. O nosso método consegue melhorar as taxas de verdadeiro positivo em uma média de 4,4, exigindo até 65% dos custos com processamento de inferência.

### Explicação da estrutura de diretórios


* `./apks/`: armazena os arquivos de APK e dois arquivos que listam os arquivos de APK utilizados no experimento:
  * `./apks/goodware/`: armazena arquivos de APK classificados como goodware obtidos pela plataforma AndroZoo. Não será utilizado na reprodução do experimento por conta da inviabilidade de tempo para download dos arquivos;
  * `./apks/malware/`: armazena arquivos de APK classificados como malware obtidos pela plataforma AndroZoo. Não será utilizado na reprodução do experimento por conta da inviabilidade de tempo para download dos arquivos;
  * `./apks/0.lista-apk-goodware.txt`: lista dos arquivos APK, classificados como goodware, identificados pelo hash. O hash do arquivo pode ser utilizado para download do arquivo na plataforma *AndroZoo* e para consultar o arquivo na plataforma *VirusTotal*;
  * `./apks/0.lista-apk-malware.txt`: lista dos arquivos APK, classificados como malware, identificados pelo hash. O hash do arquivo pode ser utilizado para download do arquivo na plataforma *AndroZoo* e para consultar o arquivo na plataforma *VirusTotal*;
* `./csv/`: armazena arquivos cvs utilizados na criação dos datasets para cada view (*API Calls*, *Opcodes*, Permissões). Esses arquivos não serão utilizados na reprodução do experimento por conta da inviabilidade de tempo;
* `./dumps/`: armazena arquivos do tipo `pkl`, que são *dumps* de algumas etapas do experimento. Eles são utilizados para tornar a reprodução do experimento viável em relação ao tempo de processamento. No entanto, em virtude do tamanho dos arquivos, foi disponibilizado o vetor com os resultados em formato `npy`.
* `./features/`: armazena arquivos intermediários, que são gerados a partir da extração das *features* dos arquivos APK e são utilizados na geração do csv; Esses arquivos não serão utilizados na reprodução do experimento por conta da inviabilidade de tempo;
* `./npy/`: armazena arquivos do tipo *numpy* (`ndarray`), os quais são utilizados para reduzir requisitos de processamento e tempo em algumas etapas do experimento. Eles são utilizados para torna a reprodução do experimento viável em relação ao tempo de processamento;
* `./src/`: armazena todos os códigos fontes utilizados no experimento, dentre esses os códigos que devem ser utilizados para reprodução do experimento;
  * `./src/outros-arquivos-do-experimento/`: armazena os códigos que foram utilizados no experimento, mas que não serão utilizados para reproduzi-lo em virtude da inviabilidade de tempo;
  * `./src/para-reproducao-experimento/`: armazena os códigos necessários para reprodução do experimento;
  * `./src/teste-dependencias.ipynb`: arquivo de código utilizado para verificar se as dependências para reprodução do experimento estão disponíveis na estrutura de diretórios;
* `./requirements.txt`: arquivo de dependências para o gerenciador de pacotes PIP.


### Instalação das dependências, download de arquivos e teste inicial

#### Instalação das dependências

O experimento utilizou VSCode v.1.88.1, Python v.3.10.12. Após esses requesitos serem atendidos e os arquivos do repositório estiverem em um ambiente para reprodução, é preciso seguir os passos abaixo:

* Abrir o terminal no diretório raiz do repositório para criação do ambiente virtual do python. O comando utilizado para criação é `python3 -m venv .venv`;
* No terminal, habilitar o ambiente virtual utilizando o comando: `source .venv/bin/activate`;
* No terminal, instalar as dependências utilizando o comando: `python -m pip install -r requirements.txt`;

#### Download de arquivos

Alguns arquivos foram criados para viabilizar a reprodução do experimento por conta do elevado tempo de processamento de algumas etapas. Esses arquivos devem ser obtidos confome descrição abaixo:

* *dumps nsga*: são os resultados do processamento dos algoritmos genéticos e necessários para obtenção dos resultados do artigo. Eles são obtidos por este [endereço](https://drive.google.com/drive/folders/1tLD21KOZFV4duZ9NzbxnwammLwgF3Oeg?usp=sharing) e devem ser salvos no diretório `./dumps/`. O resultado esperado são 3 arquivos, conforme descrito abaixo:
  * `./dumps/nsga2-maj-vot-dt.npy`
  * `./dumps/nsga2-maj-vot-knn.npy`
  * `./dumps/nsga2-maj-vot-rf.npy`
* numpy: são arquivos necessários para execução dos classificadores e necessários para obtenção dos resultados do artigo. Eles são obtidos por este [endereço](https://drive.google.com/drive/folders/1Dj_pOtJYFZLC3iMr_8QdbYqgIddE_TpI?usp=sharing) e devem ser descompadctados e salvos no diretório `./npy/`. O resultado esperado são 6 arquivos, conforme descrito abaixo:
  * `./npy/apicalls-x-pca-ordered.npy`
  * `./npy/apicalls-y-full-ordered.npy`
  * `./npy/opcodes-x-pca-ordered.npy`
  * `./npy/opcodes-y-full-ordered.npy`
  * `./npy/perm-x-pca-ordered.npy`
  * `./npy/perm-y-full-ordered.npy`

**Os arquivos citados acima são necessários para reprodução do experimento**. 

Caso seja do interesse, para verificação de outras etapas do experimento, estão disponíveis para download os seguintes arquivos:
* csv: arquivos utilizados para criação dos datasets. Eles são gerados a partir das características extraídas dos arquivos APK. Podem ser obtidos no [endereço](https://drive.google.com/drive/folders/1DG86vQtehV0HNjjFT1ivaf6HijDWqzFF?usp=sharing) e podem ser salvos no diretório `./csv/`;
* *features*: arquivos intermediários entre a etapa de extração das *features* pelo *AndroPyTool* e a criação dos *datasets*. Podem ser obtidos no [endereço](https://drive.google.com/drive/folders/1EKja5JCG7aLwIDjCmQuFADdB1cLI1c1U?usp=sharing) e podem ser salvos no diretório `./features/`. Atenção que a quantidade de arquivos no zip totaliza 120 mil arquivos.

Os arquivos citados acima **não** são necessários para reprodução do experimento.

Eles exigem cerca de 15 gigabytes de armazenamento em disco.


#### Teste inicial

Para verificação dos requisitos necessários para reprodução do experimento foi disponibilizado um arquivo de teste acessado [aqui](./src/teste-dependencias.ipynb). Dois testes são realizados: (i) se todas as bibliotecas utilizadas na reprodução do experimento estão instaladas; (ii) se os arquivos estão disponíveis nos diretórios;

Na primeira execução do *notebook* *Jupyter*, será solicitado que o *kernel* para o *notebook* seja selecionado. **Atenção para selecionar o kernel do ambiente virtual** criado nesta [etapa](#instalação-das-dependências).


### Tutorial para reprodução do experimento

Esta seção restringi-se a descrever as etapas para reprodução do experimento. Algumas etapas realizadas no processo inicial não estão descritas aqui por conta da inviabilidade de tempo na execução delas.

#### Classificação de malware para *Android* sem seleção de características

Para a realização dessa etapa, foram disponibilizados três arquivos de código *notebook Jupyter*:

* [2.1.ml_apicalls_pca.ipynb](./src/para-reproducao-experimento/2.1.ml_apicalls_pca.ipynb)
* [2.2.ml_opcodes_pca.ipynb](./src/para-reproducao-experimento/2.2.ml_opcodes_pca.ipynb)
* [2.3.ml_permissions_pca.ipynb](./src/para-reproducao-experimento/2.3.ml_permissions_pca.ipynb)

O processo básico nos três arquivos consiste em: 
* Carregar dois arquivos *numpy* (`ndarray`) que representam o *dataset*: um representa a coluna de classificação dos arquivos de APK; outro representa as características;
* Aplicar a divisão em datasets de treino e teste;
* Treinar e testar os classificadores RF, DT, kNN;
* Processar as métricas;
* Apresentar os resultados;

Cada um dos arquivos trabalha com uma única *view* (*Api calls*, *Opcodes*, Permissões), sem utilização de seleção de características.

#### Classificação de malware para *Android* com seleção de características

Para a realização dessa etapa, foram disponibilizados três arquivos de código *notebook Jupyter*:
* [3.1.nsga2-voting-dt.ipynb](./src/para-reproducao-experimento/3.1.nsga2-voting-dt.ipynb)
* [3.2.nsga2-voting-knn.ipynb](./src/para-reproducao-experimento/3.2.nsga2-voting-knn.ipynb)
* [3.3.nsga2-voting-rf.ipynb](./src/para-reproducao-experimento/3.3.nsga2-voting-rf.ipynb)

O processo básico nos três consiste em:
* Carregar 6 arquivos *numpy* (`ndarray`) que representam os *datasets* de cada *view*: um representa a coluna de classificação dos arquivos de APK; outro representa as características;
* Determinar um problema que será otimizado pelo algoritmo NSGA2. No nosso experimento o problema é composto de dois objetivos: reduzir o tempo de processamento e aumentar a acurácia;
* Aplicar a divisão em datasets de treino e teste de acordo com a seleção de características retornada pelo algoritmo NSGA2;
* Treinar e testar os classificadores RF, DT, kNN. Cada arquivo executa um único classificador para as três *views*;
* Na reprodução do experimento, não será executado a função de otimização por conta da inviabilidade de tempo. No entanto, para tornar viável a reprodução é carregado um arquivo *dump* do resultado da otimização do NSGA2;
* Processar as métricas;
* Apresentar os resultados;

Cada um dos arquivos trabalho com *multi-view* (*Api calls*, *Opcodes*, Permissões) e para um único classifidor.



### Explicações de outros processos do experimento

Esta seção encontra-se explicações de outros processos do experimento que foram omitidos da seção [Tutorial para reprodução do experimento](#tutorial-para-reprodução-do-experimento) por inviabilidade de tempo.

#### Obtenção dos arquivos APK

A reprodução desta fase do experimento requereria cerca de 8 semanas, utilizando um computador com 24 gigabytes de memória RAM e 8 núcleos de processamento, exigindo, além disso, em torno de 1 terabyte de armazenamento em disco apenas para os arquivos de APK. **Em virtude disso, torna-se inviável a reprodução desta etapa**. 

Não obstante, seguem algumas explicações do processo realizado:

O experimento utilizou 40 mil arquivos APK, os quais foram obtidos na plataforma [AndroZoo](https://androzoo.uni.lu/). AndroZoo oforece uma [API](https://androzoo.uni.lu/api_doc) para download dos arquivos, conforme exemplo:

`curl -O --remote-header-name -G -d apikey=${APIKEY} -d sha256=${SHA256} https://androzoo.uni.lu/api/download`

Explicação dos parâmetros:

* ${APIKEY}: chave de acesso,que pode ser obtida [aqui](https://androzoo.uni.lu/access);
* ${SHA256}: identificador do arquivo APK, o qual pode ser obtido por uma [lista](https://androzoo.uni.lu/lists) CSV com todos os arquivos da plataforma.

Em nosso experimento, para automatizar o processo de download dos arquivos APK, foi criado um script em python disponivel [aqui](./src/outros-arquivos-do-experimento/1.2.download-apk.py). Nesse script, aplica-se um filtro à lista CSV e em seguida escolhe-se aleatoriamente 40 mil arquivos de APK. 

Os arquivos de APK *goodware* estão listados [aqui](./apks/0.lista-apk-goodware.txt), enquanto os arquivos malware listados [aqui](./apks/0.lista-apk-malware.txt).
Cada um dos arquivos serão salvos com o identificador hash, que o identifica no CSV e também na plataforma [VirusTotal](https://www.virustotal.com). 

Como exemplo: `0113A5F7999C227F2AACB7267CDBF5321031CC6B6D39B8F5016EC169A9446F39.apk`

Caso seja de interesse, está disponível um código fonte para download dos arquivos utilizando as listas supramencionadas neste [arquivo](./src/outros-arquivos-do-experimento/1.1.download-apk-por-lista.py).

#### Análise estática dos arquivos APK

Para extração das características dos arquivos APK foi utilizada a ferramenta [*AndroPyTool*](https://github.com/alexMyG/AndroPyTool). A instalação pode ser feita via [*docker*](https://docs.docker.com/engine/install/), com o comando:

`docker pull alexmyg/andropytool`

A extração das características foi feita com os comandos: 

`docker run --volume=./apks/goodware/:/apks alexmyg/andropytool -s /apks/ -fw`

`docker run --volume=./apks/malware/:/apks alexmyg/andropytool -s /apks/ -fw`

*AndroPyTool* criará [subdiretórios](https://github.com/alexMyG/AndroPyTool?tab=readme-ov-file#input-and-output-folder-structure), sendo o mais relevante ao experimento o diretório `/Features_files/`. 

Nele são salvos os arquivos com as características estáticas dos arquivos APK em formato `json`. Cada arquivo terá como nome o identificador hash do arquivo APK, por exemplo: `0113A5F7999C227F2AACB7267CDBF5321031CC6B6D39B8F5016EC169A9446F39-analysis.json`

#### Extração das *features* por *view* a partir dos arquivos de características

Nesta fase do experimento, cada um dos arquivos com as características é processado para gerar três arquivos:

* `*-analysis-permissions.csv`: arquivo com as características da *view* permissão;
* `*-analysis-apicalls.csv`: arquivo com as características da *view* *apicalls*;
* `-analysis-opcodes.csv`: arquivo com as características da *view* *opcodes*;

Como exemplo:
* `0113A5F7999C227F2AACB7267CDBF5321031CC6B6D39B8F5016EC169A9446F39-analysis-permissions.csv`
* `0113A5F7999C227F2AACB7267CDBF5321031CC6B6D39B8F5016EC169A9446F39-analysis-apicalls.csv`
* `0113A5F7999C227F2AACB7267CDBF5321031CC6B6D39B8F5016EC169A9446F39-analysis-opcodes.csv`

Em cada um dos arquivos é incluído uma coluna chamada `class`. Se o arquivo processado for um *goodware*, `class = 0`. Se o arquivo processado for um *malware*, `class = 1`.

Para automação deste processo, foi criado o script [extracao-features](./src/outros-arquivos-do-experimento/1.3.extracao-features.py).

#### Geração do dataset

Nesta fase foram criados três *datasets*, os quais serão utilizados nos modelos de classificação. Eles são estruturados da seguinte forma:

* Cada um dos *datasets* representa uma *view* (permissões, *api calls*, *opcodes*);
* Cada linha representa um arquivo de APK;
* Cada coluna representa uma característisca do arquivo de APK;
* A coluna class representa a classificação do arquivo de APK (`*goodware* = 0`, `*malware* = 1`);
* Pode ocorrer situações em que uma característica está presente em um arquivo e não em outro. Nestes casos, caso um arquivo de APK não possua a característica, na linha deste arquivo a característica estará com o valor gerado.

Em virtude da exigência de recursos computacionais, esta etapa foi feita em algumas fases:

* geração do csv para *opcodes*. Código fonte disponível neste [arquivo](./src/outros-arquivos-do-experimento/1.3.create_csv_opcodes.ipynb);
* geração do csv para permissões. Código fonte disponível neste [arquivo](./src/outros-arquivos-do-experimento/1.3.create_csv_perms.ipynb);
* geração do csv para *api calls*. Esse processo foi divido em vários arquivos, os quais foram sendo concatenados, até a geração do *dataset* com 40 mil linhas e cerca de 65 mil características. Os arquivos estão disponíveis neste [diretório](./src/outros-arquivos-do-experimento/1.3.create_csv_apicalls/).

#### Geração dos arquivos *numpy*

Esta etapa também foi omitida da reprodução do experimento por conta da inviabilidade de tempo. Nela os seguintes passos são feitos:

* Carregar os arquivos csv de cada *view*;
* Preencher os campos NA com 0;
* Excluir colunas geradas no processo de concatenação dos datasets na fase de geração dos csv;
* Separar o *dataset* em outros dois: um apenas com a coluna de classificação, outro com as características;
* Transformar os dois *datasets* em `ndarray`;
* Aplicar PCA no ndarray das características;
* Gerar dois arquivos .npy. Esses arquivos são utilizados como `input` nas etapas de classificação.

Os arquivos utilizados nesta etapa são:

* [Permissões](./src/outros-arquivos-do-experimento/1.4.normalizacao-pca--permissions.ipynb)
* [*Api calls*](./src/outros-arquivos-do-experimento/1.4.normalizacao-pca-apicalls.ipynb)
* [*Opcodes*](./src/outros-arquivos-do-experimento/1.4.normalizacao-pca-opcodes.ipynb)



