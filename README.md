# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<a href= "https://www.fiap.com.br/"><img src="assets/logo-fiap.png" alt="FIAP - Faculdade de Informática e Admnistração Paulista" border="0" width=40% height=40%></a>
</p>

<br>

# Nome do projeto - Explorando SQL e Tipos de Dados Oracle
![gif](https://github.com/IolandaManzali/ExplorandoSQL/blob/main/assets/gitgif.gif)


## Nome do grupo - Grupo 06

## 👨‍🎓 Integrantes: 
- <a href="https://www.linkedin.com/in/hilmar-marques-358672161">Hilmar Gomes Marques da Silva</a>
- <a href="https://www.linkedin.com/in/iolanda-helena-fabbrini-manzali-de-oliveira-14ab8ab0">Iolanda Helena Fabbrini Manzali de Oliveira</a>
- <a href="https://www.linkedin.com/company/inova-fusca">Murilo Carone Nasser</a> 
- <a href="https://www.linkedin.com/in/pedro-eduardo-soares-de-sousa-439552309">Pedro Eduardo Soares de Sousa</a> 
- <a href="https://www.linkedin.com/company/inova-fusca">Yago Brendon Iama</a>

## 👩‍🏫 Professores:
### Tutor(a) 
- <a href="https://www.linkedin.com/in/lucas-gomes-moreira-15a8452a">Lucas Gomes Moreira</a>
### Coordenador(a)
- <a href="https://www.linkedin.com/company/inova-fusca">Andre Godoi Chaviato</a>

## 📜 Descrição

Para essa atividade foi criado um Modelo Entidade Relacionamento baseado na base de dados da CONASB relacionados à serie historica de safras cafeeiras entre 2014 a 2024. 

O cafe, alem de fazer parte da história e da cultura brasileira, ocupa lugar de destaque nos mercados nacional e internacional.

Selecionados os graos do tipo Arabica e Conillon pelas suas caracteristicas peculiares de plantio e caracteristicas de consumo. 

Foram colhidas informacoes sobre areas de plantio, produtividade e produçao dos grãos citados acima. 

Para  ano de 2024 os valores sao estimativos, levando-se em conta o mes de setembro de 2024.

Etapas do projeto:

 	* Analise dos dados e download das planilhas so site da CONAB.
	 
	* Criaçao do DER (Diagrama Entidade Relacionamento) utilizando o SQL Data Modeler 
	
	* Criação do MER e aplicadas as regras de design e normatização com o SQL Data Modeler 

	* Exportação do código gerado em .ddl para utilização no SQL Developer 

	* Criação do Banco de Dados pelo SQL DEveloper Oracle

	* Criação de um Dicionario de Dados em Excel, descrevendo as Entidades/Tabelas, seus tipos de dados e chaves.

	* Utilização do código criado para realização de consultas relevantes sobre os dados coletados.     
  
   
## 📁 Estrutura de pastas

Dentre os arquivos e pastas presentes na raiz do projeto, definem-se:

- <b>.github</b>: Nesta pasta ficarão os arquivos de configuração específicos do GitHub que ajudam a gerenciar e automatizar processos no repositório.

- <b>assets</b>: aqui estão os arquivos relacionados a elementos não-estruturados deste repositório, como imagens.

- <b>config</b>: Posicione aqui arquivos de configuração que são usados para definir parâmetros e ajustes do projeto.

- <b>document</b>: aqui estão todos os documentos do projeto que as atividades poderão pedir. Na subpasta "other", adicione documentos complementares e menos importantes.

- <b>scripts</b>: Posicione aqui scripts auxiliares para tarefas específicas do seu projeto. Exemplo: deploy, migrações de banco de dados, backups.

- <b>src</b>: Todo o código fonte criado para o desenvolvimento do projeto ao longo das 7 fases.

- <b>README.md</b>: arquivo que serve como guia e explicação geral sobre o projeto (o mesmo que você está lendo agora).

## 🔧 Como executar o código

 * Acessar o SQL Developer, connectar-se a um banco de dados e abrir a Query
  	
 * Acessar o conteudo das tabelas através do comando:

    	SELECT * FROM nome_da_tabela

 * Utilizar os dados das tabelas para gerar analise de dados sobre producao, produtividade e area plantada conforme os exemplos a seguir:

 * Analises por cultura e região 	
	
 * ranking de produção por região (em ordem descrescente)
	
		SELECT t2.nm_regiao, t1.nm_cultura, SUM(t3.vl_producao) AS total_producao
 		FROM t_cultura t1
		JOIN t_relatorio_cultura t3 ON t1.id_cultura = t3.id_cultura
		JOIN t_regiao t2 ON t2.cd_regiao = t3.cd_regiao
		GROUP BY t2.nm_regiao, t1.nm_cultura
		ORDER BY t2.nm_regiao, total_producao DESC;

 * ranking de produtividade por tipo de grão por ano, (em ordem descrescente)

   		SELECT t2.nm_regiao, AVG(t3.vl_produtividade) AS produtividade_media
		FROM t_cultura t1
		JOIN t_relatorio_cultura t3 ON t1.id_cultura = t3.id_cultura
		JOIN t_regiao t2 ON t2.cd_regiao = t3.cd_regiao
		WHERE t1.nm_cultura = 'tipo_de_grao' AND t1.id_ano_safra = ano_da_safra
		GROUP BY t2.nm_regiao
		ORDER BY produtividade_media DESC;
    	
	
 * comparação das produtividades médias por tipo de grão por região

	  	SELECT t2.nm_regiao,
       		AVG(CASE WHEN t1.nm_cultura = 'ARABICA' THEN t3.vl_produtividade END) AS produtividade_arabica,
       		AVG(CASE WHEN t1.nm_cultura = 'CONILLON' THEN t3.vl_produtividade END) AS produtividade_conillon
		FROM t_cultura t1
		JOIN t_relatorio_cultura t3 ON t1.id_cultura = t3.id_cultura
		JOIN t_regiao t2 ON t2.cd_regiao = t3.cd_regiao
		GROUP BY t2.nm_regiao;

 * analise da producao do café por tipo de grão entre 2014 e 2024

		SELECT t1.id_ano_safra, SUM(t3.vl_producao) AS total_producao_arabica
		FROM t_cultura t1
		JOIN t_relatorio_cultura t3 ON t1.id_cultura = t3.id_cultura
		WHERE t1.nm_cultura = 'Ttipo_de_grao'
		GROUP BY t1.id_ano_safra
		ORDER BY t1.id_ano_safra;



## 🗃 Histórico de lançamentos

* 0.5.0 - XX/XX/2024
    * 
* 0.4.0 - XX/XX/2024
    * 
* 0.3.0 - XX/XX/2024
    * 
* 0.2.0 - 30/10/2024   ![image](https://img.shields.io/badge/{Version 1.2}-{RED}?style=for-the-badge&logo={Version 1.2}&logoColor=white)
    * 
* 0.1.0 - 04/10/2024
    *

## 👨‍💻 Desenvolvedores

![grupo](https://github.com/IolandaManzali/decolando_com-_ciencia_de_dados_grupo21/blob/main/assets/grupo_fiap.jpg)


## 📋 Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/agodoi/template">MODELO GIT FIAP</a> por <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://fiap.com.br">Fiap</a> está licenciado sobre <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">Attribution 4.0 International</a>.</p>


