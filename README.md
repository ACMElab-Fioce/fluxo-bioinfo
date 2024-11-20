# fluxo-bioinfo
# Obtenção dos dados
É utilizado o BaseSpace da Illumina para obter o arquivo de sequenciamento das amostras em formato.fastq e a sequência de referência é procurada no site do NCBI e obtida em arquivo .fasta
# Pré-processamento
A ferramenta FASTP é utilizado para fazer o controle de qualidade das bases da sequência, removendo reads e realizando trimagem de bases de qualidade baixa. Além disso, ela também gera relatórios detalhados de qualidade. Nessa etapa, a sequência de referência obtida através do NCBI também é indexada utilizando o BWA index, para garantir a organização da sequência.
# Alinhamento 
O BWA mem é utilizado para alinhar a sequência das amostras à referência, gerando um arquivo .SAM que vai ser convertido para o .BAM (a forma binária) com o Samtools View.
# Indexação 
O Samtools sort + index é utilizado para compactar, ordenar e indexar o arquivo BAM, para que a sequência seja ordenada por posição genômica.
# Chamada de Variantes
O Samtools mpileup é utilizado para processar o arquivo .BAM indexado e para gerar um arquivo .BCF. As variantes são identificadas (como SNPs, deleções ou inserções) através do Bcftools call, gerando o arquivo .VCF
# Consenso
O Bcftools index é utilizado para indexar os arquivos .VCF e uma sequência consenso é gerada usando o Bcftools consensus em formato .fasta
