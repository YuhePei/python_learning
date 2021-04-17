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
### read excel with several sheets
```
excel_reader=pd.ExcelFile('six_samples_gene.xlsx')  # 指定文件
sheet_names = excel_reader.sheet_names  
sheet_names

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
### read table and naming 
```
k_number=pd.read_table('ko00001.keg',header=None,sep='  ',names=['hierarchy','k_number','kegg_info'])
k_number.dropna(axis=0, how='any', inplace=True)
```
### write dataframes to excel with several sheets
```
writer = pd.ExcelWriter('six_gene_info_plus.xlsx')
for i in range(0,6):
    df_gene[i].to_excel(writer,sheet_names[i],index=False)
writer.save()
```
