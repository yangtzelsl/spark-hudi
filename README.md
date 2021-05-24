## Source code Examples

This repo contains source code examples to go along with my blog post

https://olivermascarenhas.com/2020-04-13-building-analytical-datalake-with-apache-spark-and-apache-hudi/

## 测试效果

### 测试说明
以albumId，title作为主键，以updateDate作为分区字段，进行更新前后的对比

### 更新前数据

|_hoodie_commit_time|_hoodie_commit_seqno|_hoodie_record_key|_hoodie_partition_path|_hoodie_file_name|albumId|title|tracks|updateDate|
|:----|:----|:----|:----|:----|:----|:----|:----|:----|
|20210524120341|20210524120341_0_2|albumId:800,title...|18231|e581405e-b758-4d2...|800|6 String Theory|[Lay it down, Am ...|18231|
|20210524120341|20210524120341_0_3|albumId:800,title...|18231|e581405e-b758-4d2...|800|6 String Theory jj|[Lay it down, Am ...|18231|
|20210524120341|20210524120341_0_4|albumId:801,title...|18231|e581405e-b758-4d2...|801|Hail to the Thief|[2+2=5, Backdrifts]|18231|
|20210524120341|20210524120341_1_1|albumId:801,title...|18233|ec0c6529-1e5d-4a5...|801|Hail to the Thief|[2+2=5, Backdrift...|18233|

### 更新后数据 

|_hoodie_commit_time|_hoodie_commit_seqno|_hoodie_record_key|_hoodie_partition_path|_hoodie_file_name|albumId|title|tracks|Inc|updateDate|Inc1|
|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|
|20210524120349|20210524120349_0_5|albumId:800,title...|18231|e581405e-b758-4d2...|800|6 String Theory|[Jumpin' the blue...| |18231|null|
|20210524120341|20210524120341_0_3|albumId:800,title...|18231|e581405e-b758-4d2...|800|6 String Theory jj|[Lay it down, Am ...|null|18231|null|
|20210524120349|20210524120349_0_6|albumId:801,title...|18231|e581405e-b758-4d2...|801|Hail to the Thief|[2+2=5 ssss, Back...|ll|18231|null|
|20210524120341|20210524120341_1_1|albumId:801,title...|18233|ec0c6529-1e5d-4a5...|801|Hail to the Thief|[2+2=5, Backdrift...|null|18233|null|

### 结论
可以实现更新操作