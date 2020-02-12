# RNA-seqデータの取得・変換  
- fastqファイルを保存するディレクトリを作成  
  - ```mkdir ~/Documents/expression/seq```  
  - ```cd ~/Documents/expression/seq```  
- Runinfo Table と Accession List を上記ディレクトリにダウンロード  
- fasterq-dumpを用いてRNA-seqデータをダウンロード  
  - ```~~cat SRR_Acc_List.txt | while read line; do cmd="fasterq-dupm --split-files ${line}; gzip ${line}*fastq"; eval ${cmd}; done~~```  
- ダウンロードしたファイルを一覧  
 -  ```ls -lh *fastq.gz```  
 - ```ls -lh *fastq.gz | wc -l```  
