# Uso do arcgis-api-python para leitura e verificacao de shapefiles afim de obter uma base de dados confiavel
## Contexto:
  Antes da implementacao desse projeto , as propriedades eram incluidas manualmente por arquivos mandados por email pra mim e os kmzs eram gerados (usando o plugin [Plugin EER Fundiario](https://github.com/alex-cyberpunk/Plugins-QGIS/tree/Plugin_EER_fundiario/Plugin_EER_fundiario ) )atraves desses .shps e as metricas eram feitas por itens de uma planilha. O banco de dados geograficos apresentou ser a melhor solucao para garantir uma base confiavel onde as metricas poderiam ser feitas com mais confianca e emitir com bem mais frequencia os .kmzs pro fundiario com mais frequencia.
  Uma nova lideranca optou por ao inves de usar um banco de dados postgresql (a qual havia sido testado [antes](https://github.com/alex-cyberpunk/Postgresql))  usar o arcgis online, ja que era uma produto pronto e com suporte tecnico. 
  Dessa forma era necessario uma solucao para montar os mapas dos projetos , atualiza-los e fazer a medicao de metricas de maneira que nao causa-se mais traballho ao fundiario e ate faciltando-o se possivel. Entao foi implementado library api-python do arcgis usando o ambiente notebooks do arcgis online. De inicio foi disponibilizado apenas uma licenca creator entao adaptou-se uma solucao que ligava o sharepoint lists ( como interface onde membros do fundiario poderiam fazer e monitorar pedidos) . Capturando os anexos de shapefile por python , fazendo verificacoes e marcando o tipo de erro no shapefile e entao se aprovado , iria entrar nos feature layers e marcado como "concluido" no sharepoint e se identificado um erro (erros de status , erro de geometria, erro de interseccao) iria marcar no pedido o tipo de erro identificado. Apos isso e gerado arquivos kmzs e shapefiles atualizados que entao sao inseridos no sharepoint. A principio tambem foi implementado a insercao das areas em planilha de controle porem isso e temporario ate o sistema de contratos internos da empresa estivesse pronto , ai o arcgis iria mandar os dados pra esse sistema. 

## Fluxo executado semanalmente pela rotina : atualiza_bases.py

-Captura .shps da lista do sharepoint

-Realiza verificacoes de erro (verificando interseccoes , status ...)

-Insere informacoes nos mapas

-Emite saidas (.kmzs , .shp)

-Insere no sharepoint

*imagem esquematica do fluxograma de aprovacao dos dados geograficos da propriedade*

## Lista do sharepoint (iteracao com o fundiario ):

![image](https://github.com/alex-cyberpunk/arcgis-api-python/assets/80361639/77a80e98-93a4-4183-93a5-a8b2383472f2)
![image](https://github.com/alex-cyberpunk/arcgis-api-python/assets/80361639/8125d4c3-5599-4c74-a957-fa7286715158)

Legenda: erros roxos recusaram parte do pedido , amarelo o pedido inteiro , verdes aprovados e vermelhos ainda em aprovacao. 
Tudo isso num formato de calendario

Saidas (.shp ,.kmz , novas propriedades inseridas...):


## Sugestoes de melhorias:

1-Ao inves de usar o sharepoint lists usar algumas das solcuoes do proprio arcgis . Como por exemplo usar um site (arcgis HUB ou arcgis experienece builder )onde os topografos poderiam verificar area a area que foram mandadas a eles por um forms disponibilizados pelo proprio arcgis que pode ser usado por qualquer um. E entao alem de ser muito mais facil para os topografos verem se a interseccao era alta com outras propriedades , ele teria um monitoramento muito mais simples. So que para isso seriam necessarios uma licenca editor para cada um dos topografos e saber se seria possivel implementar um botao no site capa de executar o codigo do arcgis notebooks com o login e senha do creator . O restante da implementacao parece possivel  

