A partir de busca na literatura o seguinte workflow foi utilizado

 ([https://hbctraining.github.io/In-depth-NGS-Data-Analysis-Course/sessionVI/lessons/03_annotation-snpeff.html](https://hbctraining.github.io/In-depth-NGS-Data-Analysis-Course/sessionVI/lessons/03_annotation-snpeff.html))

### Preparando os arquivos para usar o SnpEff

bgzip;

```bash
bgzip crh22_filtered_ultimate_variants.vcf
```

Depois tabix;

```bash
tabix crh22_filtered_ultimate_variants.vcf.gz
```

 tabix na biblioteca usada para adicionar o ID, seguindo a workflow;

```bash
tabix 00-common_all.vcf.gz
```

## SnpEff

Antes de rodar o SnpEff, tentei anotar o ID no arquivo .vcf através da base de dados dbSNP (ftp://ftp.ncbi.nih.gov/snp/organisms/human_9606/VCF/) onde selecionei a pasta common_all.vcf de acordo com a legenda do NCBI que especifica que nesta biblioteca apresenta apenas variantes com MAF ≥0.01 porém as variantes do arquivo output não constaram os ID portanto presume-se que as variantes presentes no output tem um MAf < 0.01

Para rodar o SnpEff seguindo a workflow consultada, indiquei o cromossomo e a file .vcf que eu quero anotar;

```bash
./../snpEff/scripts/snpEff hg38 crh22_variants_annot.vcf > crh22_variants_annot_snpEff.vcf
```

No output constam um arquivo `.vcf` contendo as variantes anotadas, um arquivo `.txt` contendo os genes e um sumário `.html` contendo amplas informações sobre a anotação que serão usados para responder o que se pede no desafio.

### Obtenha a razão Ti/Tv (*transitions* e *transversions*) das variantes encontrada no cromossomo 22.

Ti/Tv = 2.4433

### Quantas variantes são encontradas na região de 16000000 a 20000000?

284 variantes 

### Exiba o conteúdo da linha do VCF relativa a uma variante:

Não-sinônima: 

hr22	43983958	.	A	G	225.42	PASS	AC=2;AN=2;DP=88;DP4=0,0,41,27;FS=0;MQ=60;MQ0F=0;MQSBZ=0;SGB=-0.693147;VDB=0.00386955;ANN=G|missense_variant|MODERATE|SAMM50|SAMM50|transcript|NM_015380.5|protein_coding|12/15|c.1033A>G|p.Ile345Val|1169/1692|1033/1410|345/469||	GT:PL	1/1:255,205,0

Variante no gnomAD v3.1.1 com MAF < 0.01. :

chr22	50438737	.	G	C	225.42	PASS	AC=2;AN=2;DP=59;DP4=0,0,6,35;FS=0;MQ=60;MQ0F=0;MQSBZ=0;SGB=-0.693145;VDB=0.0486888;ANN=C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001365836.1|protein_coding|21/26|c.2103G>C|p.Ala701Ala|2749/4389|2103/2901|701/966||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001242898.2|protein_coding|19/24|c.2103G>C|p.Ala701Ala|2474/4093|2103/2880|701/959||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001242899.2|protein_coding|18/23|c.2025G>C|p.Ala675Ala|2396/4015|2025/2802|675/933||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001242900.2|protein_coding|18/23|c.2022G>C|p.Ala674Ala|2393/4011|2022/2784|674/927||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351641.2|protein_coding|19/24|c.2106G>C|p.Ala702Ala|2477/4096|2106/2883|702/960||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351642.2|protein_coding|19/24|c.2103G>C|p.Ala701Ala|2474/4096|2103/2883|701/960||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351643.2|protein_coding|20/25|c.2103G>C|p.Ala701Ala|2600/4219|2103/2880|701/959||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351644.2|protein_coding|18/23|c.2022G>C|p.Ala674Ala|2393/4015|2022/2802|674/933||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351645.2|protein_coding|19/24|c.2022G>C|p.Ala674Ala|2519/4138|2022/2799|674/932||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351646.2|protein_coding|18/23|c.2019G>C|p.Ala673Ala|2390/4009|2019/2796|673/931||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351647.2|protein_coding|19/24|c.1617G>C|p.Ala539Ala|2428/4047|1617/2394|539/797||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_001351648.2|protein_coding|18/23|c.1536G>C|p.Ala512Ala|2347/3966|1536/2313|512/770||,C|synonymous_variant|LOW|PPP6R2|PPP6R2|transcript|NM_014678.5|protein_coding|18/23|c.2022G>C|p.Ala674Ala|2393/4012|2022/2799|674/932||	GT:PL	1/1:255,123,0

Dependências 

- bgzip 1.2
- tabix 1.2
- snpEff 5.0e

OBS: Adicionei dois arquivos a mais que acho interessante constar junto dos arquivos obrigatórios.