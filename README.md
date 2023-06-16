**Introducao**
  
  Antes da implementacao desse projeto , as propriedades eram incluidas manualmente por arquivos mandados por email pra mim e os kmzs eram gerados (usando o plugin desenvolvido por mim ) atraves desses .shps e as metricas eram feitas por itens de uma planilha. Eu sabia que o banco de dados geograficos era a melhor solucao para garantir uma base confiavel onde as metricas poderiam ser feitas com mais confianca e emitir com bem mais frequencia os .kmzs pro fundiario com mais frequencia.
  Apos a mudanca da minha lideranca, a nova lideranca optou de ao inves de usar um banco de dados postgresql (que eu havia testado antes) desejou usar o arcgis online, ja que era uma produto pronto. Dessa forma tive que achar uma solucao para montar os mapas dos projetos , atualiza-los e fazer a medicao de metricas de maneira que nao causa-se mais traballho ao fundiario e ate faciltando-o se possivel. Entao descobri a library api-python do arcgis a qual adaptei as solucoes. De inicio tive apenas uma licenca creator entao adaptei uma solucao que ligava o sharepoint lists ( como interface onde membros do fundiario poderiam fazer e monitorar pedidos) . Capturando os anexos de shapefile por python , fazendo verificacoes e marcando o tipo de erro no shapefile e entao se aprovado , iria entrar nos feature layers e marcado como "concluido" no sharepoint e se identificado um erro (erros de status , erro de geometria, erro de interseccao) iria marcar no pedido o tipo de erro identificado. Apos isso e gerado arquivos kmzs e shapefiles atualizados que entao sao inseridos no sharepoint. A principio tambem foi implementado a insercao das areas em planilha de controle porem isso e temporario ate o sistema de contratos internos da empresa estivesse pronto , ai o arcgis iria mandar os dados pra esse sistema. 

Fluxo executado semanalmente pela rotina : atualiza_bases.py

-Captura .shps da lista do sharepoint
-Realiza verificacoes de erro (verificando interseccoes , status ...)
-Insere informacoes nos mapas
-Emite saidas (.kmzs , .shp)
-Insere no sharepoint

Lista do sharepoint (iteracao com o fundiario ):

saidas (.shp ,.kmz , novas propriedades inseridas...):

Codigos de content manegement (cria os mapas base desenvolvidos nessa solucao): content_manegement.py 
