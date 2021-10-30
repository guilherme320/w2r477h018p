### Script_Dia_1

Dado o desafio a ser resolvido, achar variantes em um cromossomo tendo um genoma de referência, depois de muita consulta na literatura pois, não tenho experiência prévia em genotipagem de genomas/cromossomos, encontrei um workflow no site: [https://datacarpentry.org/wrangling-genomics/04-variant_calling/index.html](https://datacarpentry.org/wrangling-genomics/04-variant_calling/index.html) onde estudei as pipe lines e os softwares usados para então aplicar no desafio.

Depois de baixar e descompactar o genoma de referência, as leituras de sequenciamento e o gabarito contendo.

Primeiro paço - indexar o genoma de referência usando o software `BWA`, para que o alinhamento seja feito rapidamente, encontrando locais de alinhamento em potencial.

Usando a seguinte pipeline (a pasta onde organizei os arquivos é a "teste");

`./../bwa-0.7.17/bwa index ~/teste/grch38.chr22.fast`

Após indexar o genoma de referência, fiz o alinhamento das reads contra o mesmo, usando o algorítimo MEM do software BWA;

`./../bwa-0.7.17/bwa mem grch38.chr22.fasta ./../amostra-lbb_R1.fq ./../amostra-lbb_R2.fq > ~/teste/results/sam/aligment.sam`

O output no formato SAM será convertido em BAM, usei o software samtools como descrito no workflow, usando o comando view informando o formato do input e output ;

`~/teste/samtools-1.14/samtools view -S -b sam/aligment.sam > bam/aligments.bam`

Em seguida ordenei as variantes ainda usando o `samtools` ;

`~/teste/samtools-1.14/samtools sort -o ~/teste/results/bam/sorted.bam ~/teste/results/bam/aligments.bam`

Utilizando o software bcftools para calcular a cobertura das reads, para termos um arquivo com a informação de cobertura de cada base, seguindo o workflow;

`./../../bcftools-1.14/bcftools mpileup -O b -o ~/teste/results/bcf/crh22_raw.bcf -f ~/teste/bwa_data/grch38.chr22.fasta ~/teste/results/bam/sorted.bam`

E finalmente para identificar as variantes (SNVs) usando o bcftools usando call, informando a ploidia do genoma, o output apenas sendo das variantes e o arquivo de saída.

`./../../bcftools-1.14/bcftools call --ploidy 2 -m -v -o ~/teste/results/bcf/crh22_variants.vcf ~/teste/results/bcf/crh22_raw.bcf`

Olhando o arquivo de saída e conferindo se bate com o "pequeno-gabarito.vcf" reparei que são muitos SNVs (single nucleotide variation) podendo ou não conter SNPs (single nucleotide polymorphism) e para a verificação seria necessário um estudo envolvendo uma população de indivíduos e observar se essas variações ocorrem em toda uma população e não somente em um único indivíduo. 
Dependências 

- BWA 0.11.7
- Samtools 1.9
- BCFtools 1.8

Link para a workflow consultada - https://datacarpentry.org/wrangling-genomics/04-variant_calling/index.html
