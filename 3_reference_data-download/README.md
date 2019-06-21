# リファレンスデータのダウンロード  
## リファレンスシークエンスデータのダウンロード（STARを使う場合）
- Ensemblのデータベースにアクセス  
  - ```lftp ftp.ensembl.org/pub/release-95/fasta```  
- データの一覧表示  
  - ```ls```  
- ヒトのデータにアクセス  
  - ```cd homo_sapiens/dna```  
  - ```ls```  
- lftpを終了
  - ```exit```  
- リファレンスデータを保存するディレクトリを作成  
  - ```mkdir -p ~/Documents/expression/ref```  
  - ```cd ~/Documents/expression/ref```  
- ensemblにアクセス  
  - ```lftp ftp.ensembl.org/pub/```  
  - ```ls```  
  - ```cd release-95```  
  - ```cd fasta```  
  - ```cd homo_sapiens```  
  - ```cd dna```  
- データをダウンロード  
  - ```get Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz```  
- ダウンロードが完了したらlftpを終了
  - ```exit```  
## アノテーションデータのダウンロード（STARを使う場合）  
- Ensemblデータベースにアクセス・ダウンロード
  - ```lftp ftp.ensembl.org/pub/release-95/gtf/homo_sapiens```  
  - ```ls```  
  - ```get Homo_sapiens.GRCh38.95.gtf.gz``` 
  - ```exit # ダウンロードが完了したら```  
## 圧縮ファイルを解凍
- 一部のツールは圧縮ファイルを直接読み込めないので解凍しておく
  - ```gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz```  
  - ```gunzip Homo_sapiens.GRCh38.95.gtf.gz``` 
## リファレンスシークエンスデータのダウンロード（kallistoを使う場合）
- cDNAのリファレンスシークエンスデータを使用する
- Ensemblデータベースにアクセス・ダウンロード
  - ```lftp ftp.ensembl.org/pub/release-95/fasta/homo_sapiens/cdna```  
  - ```ls```  
  - ```get Homo_sapiens.GRCh38.cdna.all.fa.gz```  
  - ```exit # ダウンロードが完了したら```  
## 遺伝子IDと遺伝子名の対応表の作成  
- データを保存するディレクトリへ移動  
  - ```cd ~/Documents/expression/ref```  
- Rを起動  
  - ```R```  
- __以下はRのコマンド__  
  - ```if (!requireNamespace("BiocManager", quietly = TRUE))```  
  - ```install.packages("BiocManager")```  
  - ```BiocManager::install("biomaRt")```  
- パッケージのインストール  
  - ```install.packages("dplyr")```  
  - ```library(dplyr)```  
- 対象種のDataset名を確認  
  - ```ensembl = biomaRt::useEnsembl(biomart="ensembl")```  
  - ```biomaRt::listDatasets(ensembl)```  
  - ヒトの場合は58行目、__hsapiens_gene_ensembl__というdataset名であることがわかる。行はversionによって異なるので注意。  
- 遺伝子IDと遺伝子名の対応情報を取得  
  - ```mart <- biomaRt::useMart(biomart = "ENSEMBL_MART_ENSEMBL", dataset = "hsapiens_gene_ensembl", host = 'ensembl.org')```
  - ```t2g <- biomaRt::getBM(attributes = c("ensembl_transcript_id", "ensembl_gene_id", "external_gene_name"), mart = mart)```
  - ```t2g <- dplyr::rename(t2g, target_id = ensembl_transcript_id, ens_gene = ensembl_gene_id, ext_gene = external_gene_name)```  
  - ```t2g[t2g[,3] == "","ext_gene"] <- "NA"```  
- 内容を確認する  
  - ```head(t2g)```  
- 保存する  
  - ```write.table(t2g, "target2gene.txt", sep="\t",quote=F,row.names=F)```  
- Rを終了する  
  - ```q()```  
  - Save workspace image? [y/n/c]: と聞かれる。作業内容を記録したい場合は y を、記録不要の場合は n を入力してエンター



