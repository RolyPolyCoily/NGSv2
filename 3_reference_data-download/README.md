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
- ダウンロードが終了したらlftpを終了
  - ```exit```  
## アノテーションデータのダウンロード（STARを使う場合）  
- Ensemblデータベースにアクセス・ダウンロード
  - ```lftp ftp.ensembl.org/pub/release-95/gtf/homo_sapiens```  
  - ```ls```  
  - ```get Homo_sapiens.GRCh38.95.gtf.gz``` 
  - ```exit```  
## 圧縮ファイルを解凍
- 一部のツールは圧縮ファイルを直接読み込めないので解凍しておく
  - ```gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz```  
  - ```gunzip Homo_sapiens.GRCh38.95.gtf.gz``` 

## 
