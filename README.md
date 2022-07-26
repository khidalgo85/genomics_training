
<!-- README.md is generated from README.Rmd. Please edit that file -->
<!-- badges: start -->

![forthebadge](https://img.shields.io/badge/GEMM-Building-orange)
![forthebadge](https://forthebadge.com/images/badges/built-with-science.svg)

<!-- badges: end -->

# Tutorial para análises de genomas

**Autores: MsC. Kelly Hidalgo** **MsC. Luis Gabriel Cueva Yesquén**

Pipeline para montagem e anotação taxonômica e funcional de genomas de
isolados. Para este tutorial será usado como modelo um genoma
bacteriano,sequenciado na plataforma Illumina (2 x 250 bp). As análises
serão conduzidas seguindo duas abordagens, baseados em linha de comando
(CLI *Command Line Interface*) e usando ferramentas online (GUI
*Graphical User Interface*).

------------------------------------------------------------------------

# WORKFLOW

<img src="imgs/workflow.png" align="center"/>

## 0. Organização de Dados

### 0.1. Login no servidor

Para os usuários baseados em Windows é necessário a instalação do
software
[MobaXterm](https://mobaxterm.mobatek.net/download-home-edition.html#:~:text=MobaXterm%20Home%20Edition%20v22.1%0A(Installer%20edition)).

Após instalado, clique na opção *session*, escolha o icone ssh e
preencha com os dados do login: *remote host* (endereço IP). Depois
selecione a opção *specify name* e preencha com o nome do usuario. Por
último será solicitada a senha. Você pode salvar os dados do login.

### 0.2. Sequências

As sequências foram obtidas do sequenciamento na plataforma Illumina
usando o protocolo *paired-end* (2 x 250 bp) de cepa bacteriana EP216.

**Arquivos**

-   `216_R1.fastq`
-   `216_R2.fastq`

> **Dica:** Usualmente os arquivos são entregues com nomes codificados
> do equipamento usado para o sequenciamento que não são informativos
> para o usuário. Sempre renomee os arquivos com palavras de fácil
> identificação. Evite espaços e caracteres especiais. Para separar
> palavras prefira *underline* `_`.

### 0.2. Criação de diretórios

Os seguintes comandos são para criar, organizar e explorar diretórios.

-   Crie um diretório base para todo o processo usando o comando `mkdir`
    (*make dir*)

<!-- -->

    mkdir genomica

-   Entre ao novo diretório usando o comando `cd` (*change directory*)

<!-- -->

    cd genomica/

-   Crie um novo diretório para armazenar as sequências brutas.

**Dica:** Dado que a maiora das etapas do workflow são sequenciais, é
recomendável nomear os diretórios começando com um número e assim manter
a organização.

    mkdir 00.RawData

-   Crie os demais diretórios em uma linha de comando só

<!-- -->

    mkdir 01.FastqcReports 02.CleanData 03.Assembly 04.QualityAssembly 05.GenePrediction 06.TaxonomyAnnotation 07.FunctionalAnnotation

-   Use o comando `ll` (*list*) para listar o conteúdo do diretório
    atual

<!-- -->

    ll

-   O comando `pwd` (*print working directory*) imprime o caminho ao
    diretório atual

<!-- -->

    pwd

### 0.3. Upload de sequências

As sequências devem ser descarregadas da plataforma da facility
contratada e subidas ao servidor usando o software MobaXterm
