# NGSv2 - Gene expression analysis
NGS教本第二版の遺伝子発現解析パート  
- はじめに  
```mkdir ~/Documents/expression```  
- RNA-seqデータの取得・変換  
```mkdir ~/Documents/expression/seq```  
```cd ~/Documents/expression/seq```  
  - ウェブブラウザでダウンロードしたSraRunTable.txtを閲覧
  ```cat SraRunTable.txt```  
  ```head -n1 SraRunTable.txt```  
  ```cut -f5,8,10,12,14,16 SraRunTable.txt```  
  - データをダウンロードする際に参照するテキストファイルを作成  
  ```tail -n+2 SraRunTable.txt | cut -f5 > run_ids```  
  - 
