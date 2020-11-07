# Comandos de la Práctica 01
## Aldair Coronel


# Parte I.


$ mkdir GenomicaComputacional

$ cd GenomicaComputacional

$ mkdir acoronel_p01

$ cd acoronel_p01

$ touch comandos_p01.md



**Respuesta 1:**

$ echo $0

>bash

**Respuesta 2:**

$ mkdir data filtered raw_data meta scripts figures archive


**Respuesta 3:**

$ mv filtered/ data/

$ mv raw_data/ data/


**Respuesta 4:**

**¿A qué se debe el nombre y la organización de los directorios que acabamos de crear?**

Dentro de la carpeta principal un proyecto bioinformático debe tener lo siguiente:

* **data** contiene datos genéticos que a su vez se pueden dividir en raw,
filtered, genotypes, etc. De este modo los datos en crudo y los modificados
están separados.

* **meta** contiene metadatos.

* **scripts** contiene los scrips necesarios para correr el análisis de principio
a fin.

* **figures** contiene código extra para hacer las figuras para la publicación, etc.

* **archive** contiene scrips y resultados que no creemos necesitar pero por si
las dudas aún los almacenamos.


# Parte II.


$ cd scripts/

$ touch delay.sh

$ which bash

>/bin/bash

$ nano delay.sh


**Respuesta 1:**

$ chmod u+x delay.sh


**Respuesta 2:**

$ ls -l

>total 4
-rwxrw-r-- 1 aldaircr aldaircr 92 Oct 28 22:25 delay.sh


**Respuesta 3:**

sleep 30


**Respuesta 4:**

$ ./delay.sh &

>[1] 31004

$ kill -9 31004

>[1]+  Killed                  ./delay.sh



# Parte III.

**Respuesta 1:**

$ cd meta/

$ touch SarsCov-2.txt


**Respuesta 2:**

$ mv sequence.fasta sarscov2_genome.fasta

$ mv sequence.gff3 sarscov2_genome.gff3

$ mv sequence\ \(1\).fasta splike_c.faa

$ mv sequence\ \(2\).fasta splike_b.faa

$ mv sequence\ \(3\).fasta splike_a.faa

$ cd meta/

$ touch SarsCov-2_Spike.txt


$ mv sarscov2_genome.fasta sarscov2_genome.gff3 splike_c.faa splike_b.faa splike_a.faa SRR10971381_R1.fastq.gz SRR10971381_R2.fastq.gz sarscov2_assembly.fasta.gz data/raw_data/



# Parte IV.

**Respuesta 1:**

$ ln -s ~/Desktop/GenomicaComputacional/acoronel_p01/data/raw_data/splike_c.faa

$ ln -s ~/Desktop/GenomicaComputacional/acoronel_p01/data/raw_data/splike_b.faa

$ ln -s ~/Desktop/GenomicaComputacional/acoronel_p01/data/raw_data/splike_a.faa


**Respuesta 2:**

$ touch glycoproteins.faa


**Respuesta 3:**

$ head -1 splike_c.faa
>pdb|6VXX|C Chain C, SARS-CoV-2 spike glycoprotein


$ head -1 splike_b.faa
>pdb|6VXX|B Chain B, SARS-CoV-2 spike glycoprotein


$ head -1 splike_a.faa
>pdb|6VXX|A Chain A, SARS-CoV-2 spike glycoprotein


**Respuesta 4:**

$ less splike_*.faa >> glycoproteins.faa


**Respuesta 5:**

Dentro de data/raw_data/

$ mv splike_*.faa ../../archive/

*¿Qué pasó con las ligas simbólicas suaves?*

*Se rompieron al momento de realizar la operación mv.*


*Intentar acceder a los archivos .gz*

$ zless sarscov2_assembly.fasta.gz


**Respuesta 6**

$ less sarscov2_genome.fasta

$ zless sarscov2_assembly.fasta.gz


*Usa el comando adecuado para ver en la terminal las primeras 3 líneas de los archivos:*

$ head -3 sarscov2_genome.fasta

>NC_045512.2 Severe acute respiratory syndrome coronavirus 2 isolate Wuhan-Hu-1, complete genome
ATTAAAGGTTTATACCTTCCCAGGTAACAAACCAACCAACTTTCGATCTCTTGTAGATCTGTTCTCTAAA
CGAACTTTAAAATCTGTGTGGCTGTCACTCGGCTGCATGCTTAGTGCACTCACGCAGTATAATTAATAAC

$ zless sarscov2_assembly.fasta.gz | head -3

>NODE_1_length_264_cov_161.042781
CACAAATCTTAACACTCTTCCCTACACGACGCTCTTCCGATCTACGCCGGGCCATTCGTA
CGAACCGATACCTGTGGTAAAGGGTCCTACTGTATGGTGGTACACGAGTAGTAGCAAATG


*¿Cómo explicas la diferencia entre el número de lecturas de los archivos .fasta?*

*A primera instancia creería que se debe a que el .gz está comprimido por ende
despliega menos información.*


**Respuesta 7:**

$ grep '>' sarscov2_genome.fasta | wc

>1      11      97

*Tiene 1 secuencia.*

$ zless sarscov2_assembly.fasta.gz | grep '>' | wc

>35      35    1171

*Tiene 35 secuencias.*


**Respuesta 8:**

$ zless SRR10971381_R2.fastq.gz | head -12

>@SRR10971381.512_2
CGTGGAGTATGGCTACATACTACTTATTTGATGAGTCTGGTGAGTTTAAAGTGGCTTCACATATGTATTGTTCTTTCTACCCTCCAGATGAGGATGAAGAAGAAGGTGATTGTGAAGAAGAAGAGTTTGAGCCATCAACTCAATATGAGT
>+
/FFFA/A/FFFF66FFFFFF/FF/FFFFFFFFFFFFF/AFFF6FFFA6FFFFF/FFFFFFFFFFFFFFFFFF/FF/FFFFFA/FFF/FFF/A/AFA/FFFFF/=F/F/F/AFAFF//A/AFF//FFAF/FFF=FFAFFFA/A/6=///==
>@SRR10971381.556_2
TTTGTAAAAATAAAATAAAAAAAATAAAAATAATATATTAAAAAAAGATAAATAAAAAAATGAACAATTAATAAAAAAAAAAAAAAAAAAAAATTAAAAAAAAAAAAAAAAAAAATAAAAAAAAAAAAAAATAAAAAAAAAATTATAAAA
>+
6AFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF/FFFAFFFFFF/FFA/FF=F//=FF/FFFFFFFFFFFFFA/FFFF/FF/FA//F/FFFFFFA/=FFFFF/FFFF/F=FFFAFF///FFFFA/FF/6//////=/
>@SRR10971381.1428_2
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
>+
>FFFFFFFFFFFFAFFFAFFFFFF6A//F//FFF


*El caracter que me podría ayudar es el arroba '@'*


$ zless SRR10971381_R2.fastq.gz | grep '@' | wc

>130022  130022 3069925


*Hay 130022 secuencias.*


**Respuesta 9:**

Explica la diferencia entre los formatos .faa, .fastqc y fasta: ¿Las secuencias
hacen referencia a nucleótidos o aminoácidos?

*¿Qué almacena cada formato?*

* **.faa:** almacena secuencias de aminoácidos.
* **.fastqc:** almaacena secuencias biológicas (generalmente secuencias de nucleótidos)
               y su correpondiente score de calidad. Tanto como la letra de secuencia
               y el score de calidad están codificados con un solo caracter ASCII.
* **.fasta:** almacena secuencias de nucleótidos.

¿A qué corresponde la información de las líneas en el formato fastqc?.

*Según el internet cada archivo .fastqc usualmente usa 4 línas para cada secuencia:*

1. La primera inicia con un arroba y seguido un identificador de secuencia, además
   de una descripcion opcional (como la línea del titulo en FASTA).
1. La segunda son las secuencias raw.
1. La tercera empieza con un '+' y por un identificador y descripcion opcional.
1. La cuarta codifica la calidad de los valores para la secuencia en la línea 2.
   Además debe contener la misma cantidad de símbolos que letras en la secuencia.

Ejemplo del internet:

>@SEQ_ID

>GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAATCCATTTGTTCAACTCACAGTTT

>+

>!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65   


**Respuesta 10:**

*Con el comando $ less sarscov2_genome.gff3:*

*El archivo se ve muy desorganizado en su lectura, tal vez sea porque se están
leyendo las líenas completas de los archivos y eso hace que no sea fácil de
entender a la vista.*


*Con el comando $ less -S sarscov2_genome.gff3:*

*El archivo se lee más claro, pareciera que se está representando como una
tabla con columnas y filas. Aunque parece que corta las lineas al momento
de llenar la pantalla.*

*Viendo lo que dice man:*

>-S or --chop-long-lines
Causes  lines longer than the screen width to be chopped (truncated) rather than wrapped.


**Respuesta 11:**

$ grep 'gene'  sarscov2_genome.gff3 -oP  | wc -l

> 75

*Hay 75 apariciones de gene.*

¿A qué corresponde el campo tres?

*Las regiones del gen.*


**Respuesta 12:**

$ git init
>Initialized empty Git repository in /home/aldaircr/Desktop/GenomicaComputacional/.git/

$ git add .

$ git commit -m "[feat] Add my computational genomics directory"

$ git remote add origin https://github.com/AldairCoronel/GenomicaComputacional-Practica01.git

$ git remote add origin https://github.com/AldairCoronel/GenomicaComputacional-Practica01.git

$ git branch -M main

$ git push -u origin main

>Username for 'https://github.com': AldairCoronel

>Password for 'https://AldairCoronel@github.com':

>Counting objects: 6, done.

>Delta compression using up to 8 threads.

>Compressing objects: 100% (4/4), done.

>Writing objects: 100% (6/6), 915 bytes | 0 bytes/s, done.

>Total 6 (delta 0), reused 0 (delta 0)

>To https://github.com/AldairCoronel/GenomicaComputacional-Practica01.git

> * [new branch]      main -> main

>Branch main set up to track remote branch main from origin.
