1- Quais variantes deverão ser desconsideradas no seu VCF? - Qualquer
métrica do software de escolha poderá ser utilizada. Discorra sobre a
métrica utilizada.

Primeiro a filtragem de SNVs do arquivo `vcf` do cromossomo 22, utilizando `bcftools`

```bash
./vcfutils.pl varFilter ~/work_space/mendelics.chalenge/dia_1/results/bcf/crh22_variants\ \(cópia\).vcf > crh22_final_variants.vcf
```

A partir de uma busca na literatura ([https://www.nature.com/articles/s41598-019-52614-7#Fig3](https://www.nature.com/articles/s41598-019-52614-7#Fig3)) usei o "GATK best practices and VQSR" onde achei o tutorial **(How to) Filter variants either with VQSR or by hard-filtering** onde preferi por usar a workflow **Hard-filter SNPs on multiple expressions using VariantFiltration**  por que se adequava aos materiais que eu tinha acesso usando as seguintes métricas QUAL / FS / MQ seguindo a workflow 

- Hard filter using gatk

```bash
 ./gatk VariantFiltration -V ../crh22_final_variants.vcf -filter "QUAL < 30.0" --filter-name "QUAL30" -filter "FS > 60.0" --filter-name "FS60" -filter "MQ < 40.0" --filter-name "MQ40" -O crh22_filtered_final_variants.vcf
```

2- Discorra sobre as regiões com baixa cobertura e quais foram seus critérios. Figuras são bem-vindas.

Para as regiões com baixa cobertura segui a recomendação de utilizar o mosdepth, apenas quantificando as regiões com baixa cobertura, utilizando a BED file que foi disponibilizada.

Primeiramente criei o Index que será necessário para utilização do mosdepth;

```bash
../dia_1/samtools-1.14/samtools index ../dia_1/results/bam/sorted.bam
```

Depois rodei a seguinte linha de código seguindo o "usage" disponibilizado no github do sofware;

```bash
~/miniconda3/bin/./mosdepth --by ../coverage.bed sample-output ../../dia_1/results/bam/sorted.bam
```

3- Obter informações sobre seu alinhamento. Quantos reads? Qual a
porcentagem deles que foi mapeada corretamente? Muitos alinharam em mais de um local do genoma com a mesma qualidade?

Para a obtenção das informações do alinhamento usei o software samtools que disponibilizou alguns os dados necessário como o `coverage` e `flagstat`;

Comando para rodar o samtools coverage

```bash
~/work_space/mendelics.chalenge/dia_1/samtools-1.14/samtools coverage ../../dia_1/results/bam/sorted.bam > samtools_coverage_crh22_sorted.bam
```

Comando para rodar o samtools flagstat

```bash
~/work_space/mendelics.chalenge/dia_1/samtools-1.14/samtools flagstat ../../dia_1/results/bam/sorted.bam > samtools_flagstats_crh22_sorted.txt
```

OBS: A maioria dos arquivos usados foram feitos no primeiro dia do desafio

Dependências 

- bcftools 1.8
- gatk 4.2.2.0
- samtools 1.9
- mostdepth 0.3.2