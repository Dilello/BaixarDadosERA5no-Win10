# Como acessar os dados do ERA5 usando python no Windows 10

ERA5 é a reanálise climática de quinta geração produzida pelo Centro Europeu de Previsões Meteorológicas de Médio Prazo (ECMWF). 
O produto fornece saída horária para muitos parâmetros atmosféricos, terrestres e oceânicos, juntamente com estimativas de incerteza. 

Esta postagem tem como objetivo descrever a instalarção da API do armazenamento de dados climáticos (CDS) para ler e analisar a saída ERA5 em Python e no sistema operacional Windows 10.

## Etapas

### 1 - Criar uma conta na [Copernicus](https://cds.climate.copernicus.eu/);

### 2 - Entrar [aqui](https://cds.climate.copernicus.eu/user) usando seu login e senha da Copernicus e obter sua UID e API Key:

Exemplo:

UID: 999999

API_KEY: fb9b99cd-9cf9-99bf-999a-e9ad999c99e9

### 3 - Copiar e salvar sua UID e API Key num bloco de notas;

### 4 - Abrir terminal e editar o codigo abaixo substituindo o UID pelo número do seu UID e o API Key pelo seu número API Key:
```
{
  
  echo 'url: https://cds.climate.copernicus.eu/api/v2'
  
  echo 'key: UID:API_KEY'
  
  echo 'verify: 0'

} > ~/.cdsapirc

```

ou abrir um bloco notas e colar seu UID e API Key conforme o exemplo:

```
url: https://cds.climate.copernicus.eu/api/v2

key: 999999:fb9b99cd-9cf9-99bf-999a-e9ad999c99e9

verify:0
```

e salvar em C:\Users\Username folder com extensão .cdsapirc

Obs.: Verficar a extensão do arquivo, caso esteja como .txt trocar por .cdsapirc

### 5 - Instalando CDS API:

```
pip install cdsapi
```
ou

```
conda install cdsapi
```

### 6 - Verificando se não houve erro até aqui, entrar no Python Script e digitar:

```python
import cdsapi

cds = cdsapi.Client()
```

### 7 - Salvar no seu diretório os códigos e arquivos disponíveis nesta [postagem](https://github.com/Dilello/BaixarDadosERA5no-Win10)


### 8 - Pré-requisitos: netCDF4

```
pip install netCDF4
```
ou

```
conda install -c conda-forge netCDF4
```

### 9 - Abrir o código [era5_crocotools_param.py](https://github.com/Dilello/BaixarDadosERA5no-Win10/blob/main/era5_crocotools_param.py) em um editor de texto da sua preferência e modificar conforme suas necessidades as linhas:

12, 13, 26, 27, 28, 29, 33, 44, 57, 58, 59, 60, 71, 72 e 73

Este código foi construído para se obter pressão ao nível do mar (Pa) e velocidade do vento a 10 m (m/s) nas componentes u e v. Caso queira outros parametros ver no [ECMWF](https://confluence.ecmwf.int/display/CKB/ERA5%3A+data+documentation#ERA5:datadocumentation-Parameterlistings) (coluna 'shortName') e incorporar nas listas das linhas 44 e 71 a 73 e na lista presente no arquivo [ERA5_variables](https://github.com/Dilello/BaixarDadosERA5no-Win10/blob/main/ERA5_variables.json). Caso de ondas: Hs é swh, Tp é pp1d e Dir é mwd.
Recomenda-se realizar download a cada 3 meses de dados. IMPORTANTE: As datas devem estar no MESMO ANO.

### 10 - Abrir o código [crocotools_param.m](https://github.com/Dilello/BaixarDadosERA5no-Win10/blob/main/crocotools_param.m) em um editor de texto da sua preferência e modificar conforme suas necessidades as linhas:

12, 13, 26, 27, 28, 29, 33, 44, 57, 58, 59, 60, 71, 72 e 73

Este código foi construído para se obter pressão ao nível do mar (Pa) e velocidade do vento a 10 m (m/s) nas componentes u e v. Caso queira outros parametros ver no [ECMWF](https://confluence.ecmwf.int/display/CKB/ERA5%3A+data+documentation#ERA5:datadocumentation-Parameterlistings) (coluna 'shortName') e incorporar nas listas das linhas 44 e 71 a 73 e na lista presente no arquivo [ERA5_variables](https://github.com/Dilello/BaixarDadosERA5no-Win10/blob/main/ERA5_variables.json). Caso de ondas: Hs é swh, Tp é pp1d e Dir é mwd.
Recomenda-se realizar download a cada 3 meses de dados. IMPORTANTE: As datas devem estar no MESMO ANO.

### 11 - Abrir o código [ERA5_request](https://github.com/Dilello/BaixarDadosERA5no-Win10/blob/main/ERA5_request.py) em um editor de texto, modificar e salvar as seguintes linhas:

83 a 86


### 12 - Já no seu diretório de trabalho executar pelo prompt do Anaconda o código [ERA5_request](https://github.com/Dilello/BaixarDadosERA5no-Win10/blob/main/ERA5_request.py):

A cada rodada, deve-se deletar a pasta DATA/ERA5_native_Teste1

```
python ERA5_request.py
```

### 13 - Já no seu diretório de trabalho executar pelo prompt do Anaconda o código [ERA5_convert](https://github.com/Dilello/BaixarDadosERA5no-Win10/blob/main/ERA5_convert.py):

A cada rodada, deve-se deletar a pasta DATA/ERA5_Teste1

```
python ERA5_convert.py
```





