# smrjan.github.io
Languages:
1. Python
2. R
3. Scala
4. Julia

Storage Tools:
1. Kite Sdk
2. eel-sdk
3. pucket

Data Storage Format:
1. Text(JSON/CSV): Fast read/write, inefficient
2. Avro: Raw based format, Schema, For medium to long term storage
3. Parquet: Column based format, Fast Query
4. ORC: Similar to Parquet, Richer data

DataBases:
1. Apache Calcite: SQL Processor
2. Apache HAWK

Big Data SQL query Tools:
1. Drill: Query unstructured data from HDFS/HBASE/CASSANDRA/S3. Format: JSON, Schema: N/A
2. Presto: Query unstructured data from HDFS/HBASE/CASSANDRA. Format: columnar, Schema: Required

Processing
1. Spark/MLLib
2. H2O.ai
⋅⋅3. MADLib

Notebook/Visualization
1. Jupyter
2. Zeppelin

EMR Cluster
/usr/bin/aws emr create-cluster --name "sss $NOW" --release-label emr-5.3.1 --log-uri s3://elasticmapreduce/ --enable-debugging --applications Name=Ganglia Name=Presto Name=Zeppelin Name=Spark --use-default-roles --ec2-attributes KeyName="toolbox" --instance-groups InstanceGroupType=MASTER,InstanceCount=1,InstanceType=m3.xlarge InstanceGroupType=CORE,InstanceCount=3,InstanceType=m3.xlarge --bootstrap-action Path=s3://bootstrapp/setup_drill

/usr/bin/aws emr create-cluster --release-label emr-5.3.1 \
  --name 'jupyter + emr-5.3.1 + $NOW' \
  --applications Name=Spark Name=Ganglia Name=Presto Name=Zeppelin \
  --ec2-attributes KeyName="toolbox",InstanceProfile=EMR_EC2_DefaultRole \
  --service-role EMR_DefaultRole \
  --instance-groups \
    InstanceGroupType=MASTER,InstanceCount=1,InstanceType=c3.xlarge \
    InstanceGroupType=CORE,InstanceCount=2,InstanceType=r3.xlarge,BidPrice=0.05 \
  --log-uri s3://sss/emr-logs/ \
  --bootstrap-actions \
    Name='Install Jupyter notebook',Path="s3://aws-bigdata-blog/artifacts/aws-blog-emr-jupyter/install-jupyter-emr5.sh",Args=[--r,--julia,--toree,--torch,--ruby,--ds-packages,--ml-packages,--python-packages,'ggplot nilearn',--port,8880,--password,jupyter,--jupyterhub,--jupyterhub-port,8001,--cached-install,--notebook-dir,s3://sss/notebooks/,--copy-samples]
