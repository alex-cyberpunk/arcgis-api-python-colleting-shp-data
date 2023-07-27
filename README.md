# Uso do arcgis-api-python para leitura e verificacao de shapefiles afim de obter uma base de dados confiavel
## Contexto:
  Context:
Before the implementation of this project, properties were manually added by receiving files sent via email, and .kmz files were generated (using the [Plugin EER Fundiario](https://github.com/alex-cyberpunk/Plugins-QGIS/tree/Plugin_EER_fundiario/Plugin_EER_fundiario )) through these .shp files, and metrics were calculated using items from a spreadsheet. The geospatial database proved to be the best solution to ensure a reliable foundation where metrics could be calculated with more confidence, and .kmz files could be generated more frequently for the fundiario department.

Under new leadership, instead of using a PostgreSQL database (which had been tested [previously](https://github.com/alex-cyberpunk/Postgresql)), the decision was made to use ArcGIS Online, as it was a ready-to-use product with technical support. Therefore, a solution was needed to create, update, and measure project maps in a way that would not add more work for the fundiario department and possibly make their tasks easier. The ArcGIS API for Python was implemented using the ArcGIS Online notebooks environment. Initially, only one creator license was available, so a solution was adapted that connected SharePoint lists (serving as an interface where fundiario members could make and monitor requests). Python was used to capture shapefile attachments, perform error checks, and mark the type of error in the shapefile. If approved, the data would enter the feature layers and be marked as "completed" in SharePoint. If an error was identified (status errors, geometry errors, intersection errors), the type of identified error would be marked in the request. After that, updated .kmz and shapefiles would be generated and inserted into SharePoint. Initially, property information was also inserted into a control spreadsheet, but this is temporary until the company's internal contract system is ready, at which point ArcGIS will send the data to that system.

## Implementation: 


### Weekly Flow executed by the routine: atualiza_bases.py

-Capture .shp files from the SharePoint list.
-Perform error checks (intersection, status, etc.).
-Insert information into maps.
-Output (.kmz, .shp).
-Insert into SharePoint.
-Diagram of the geographic property data approval flow

### SharePoint list (interaction with the fundiario department):

![image](https://github.com/alex-cyberpunk/arcgis-api-python/assets/80361639/77a80e98-93a4-4183-93a5-a8b2383472f2)
![image](https://github.com/alex-cyberpunk/arcgis-api-python/assets/80361639/8125d4c3-5599-4c74-a957-fa7286715158)

Legend: Purple indicates that part of the request was denied, yellow means the entire request was denied, green indicates approval, and red shows requests still pending approval. All displayed in a calendar format.

Outputs (.shp, .kmz, newly inserted properties, etc.):


## Suggestions for improvements:

1-Instead of using SharePoint lists, consider using some of ArcGIS's own solutions, such as using a site (ArcGIS Hub or ArcGIS Experience Builder) where topographers could check area by area, which would be sent to them through forms provided by ArcGIS that can be used by anyone. This would make it much easier for topographers to verify if the intersection with other properties is high. It would also simplify monitoring. However, this would require an editor license for each topographer, and it would be necessary to check if it's possible to implement a button on the site capable of executing the ArcGIS Notebooks code with the creator's login and password. The rest of the implementation appears feasible.

