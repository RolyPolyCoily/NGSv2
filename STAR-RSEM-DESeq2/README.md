# STAR、RSEM、DESeq2を用いた処理  
## STAR  
- ツールを保管するディレクトリへ移動  
  - ```cd ~/Documents/expression/tools```  
- STARをダウンロード・展開  
  - ```wget https://github.com/alexdobin/STAR/archive/2.7.0a.tar.gz```  
  - ```tar -xzf 2.7.0a.tar.gz```  
- 動作確認  
  - ```STAR-2.7.0a/bin/MacOSX_x86_64/STAR --version```  
- 使い方の表示  
  - ```STAR-2.7.0a/bin/MacOSX_x86_64/STAR --help```  
- インデックスの作成  
  - インデックスを出力するディレクトリを作成  
    - ```mkdir ~/Docume nts/expression/ref/STAR_reference```  
  - インデックス作成  
    - ```~/Documents/expression/tools/STAR-2.7.0a/bin/MacOSX_x86_64/STAR --runMode genomeGenerate --genomeDir ~/Documents/expression/ref/STAR_reference --genomeFastaFiles ~/Documents/expression/ref/Homo_sapiens.GRCh38.dna.primary_assembly.fa --sjdbGTFfile ~/Documents/expression/ref/Homo_sapiens.GRCh38.95.gtf```  
- マッピング  
  - マッピングしたファイルを保管するディレクトリを作成  
    - ```mkdir -p ~/Documents/expression/STAR```  
    - ```cd ~/Documents/expression/STAR```  
  - １サンプル分のマッピング（SRR\*\*\*\*\*\*\*には実在するSRR IDを記入する）
    - ```~/Documents/expression/tools/STAR-2.7.0a/bin/MacOSX_x86_64/STAR --runMode alignReads --genomeDir ../ref/STAR_reference --readFilesCommand gunzip -c --readFilesIn ../seq/SRR*******_1.fastq.gz  ../seq/SRR*******_2.fastq.gz --outSAMtype BAM SortedByCoordinate --runThreadN 4 --outFileNamePrefix SRR1550989 --quantMode TranscriptomeSAM```  
  - 多サンプルのマッピング
    - ```for sample in `ls ../seq/*fastq.gz | xargs basename | cut -f1 -d"_" | uniq`; do echo mapping:${sample}; ../tools/STAR-2.7.0a/bin/MacOSX_x86_64/STAR --runMode alignReads --genomeDir ../ref/STAR_reference --readFilesCommand gunzip -c  --readFilesIn ../seq/${sample}_1.fastq.gz ../seq/${sample}_2.fastq.gz --outSAMtype BAM SortedByCoordinate --runThreadN 4 --quantMode TranscriptomeSAM --outFileNamePrefix ${sample};done; echo finished```  
## RSEM
- source codeを ~/Documents/expression/tools にダウンロードしたのちファイルを解凍
  - ```cd ~/Documents/expression/tools```  
  - ```tar -zxvf RSEM-1.3.1.tar.gz```  
- インデックスの作成  
  - インデックス保存用のディレクトリを作成  
    - ```mkdir ~/Documents/expression/ref/RSEM_reference```  
    - ```cd ~/Documents/expression/ref/RSEM_reference```  
  - インデックス作成
    - ```../tools/RSEM-1.3.1/bin/rsem-prepare-reference --num-threads 4 --gtf Homo_sapiens.GRCh38.95.gtf Homo_sapiens.GRCh38.dna.primary_assembly.fa RSEM_reference/RSEM_reference```  
- 発現量定量


