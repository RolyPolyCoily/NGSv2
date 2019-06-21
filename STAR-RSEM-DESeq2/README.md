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
