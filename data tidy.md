### concatenate two dataframe 
```
df_cell = pd.merge(df_cell, cell_tmp_1,how='left',left_on='cellID',right_on='index')
```
### rename one colomn in dataframe
```
df_cell.rename(columns = {'cluster_ID_name':'clusterName'}, inplace=True)
```
### string concatenation
```
df_cell['title']=[ 'MP '+i.split('_')[0].split('-')[1] for i in df_cell['cellID'].tolist()]
```
### make a 3D array by dictionary
```
df_marker={}
for i in range(0,5):
    df_marker_i=pd.read_excel('../downloaded_data/mmc1.xlsx', sheet_name=sheet_names[i]) 
    df_marker[i]=df_marker_i
    print(df_marker_i)
```
### FOR statement
```
markerGenes = {}
for clusterID,clusterName in clusters.items():
    cluster_markers ={}
    cluster_markers['geneSymbol']=df_marker[clusterID]['geneID'].tolist()
    cluster_markers['ensemblID']=my_builder.calculate_ensemblID(cluster_markers['geneSymbol'])
    cluster_markers['pValue']=df_marker[clusterID]['p_val'].tolist()
    cluster_markers['statistics']=df_marker[clusterID]['avg_log2FC'].tolist()
    cluster_markers['statisticsType']=['notAvailable']*len(cluster_markers['geneSymbol'])
    markerGenes[clusterName]=cluster_markers
    print(clusterName)
```
