**向hadoop集群上传文件**  

hadoop fs -mkdir /whl # 新建文件夹  

从本地拖到Xsheel窗口  

hadoop fs -put uber-raw-data-sep14.csv /whl/ # 执行上传命令  

hadoop fs -rm -r -skipTrash /path_to_file/file_name  # 执行删除文件或文件夹  