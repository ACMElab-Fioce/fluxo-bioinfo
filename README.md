# 🔬 Fluxo Bioinformático

Este repositório descreve o **pipeline de bioinformática** utilizado para o processamento e análise de dados de **sequenciamento genômico**. O fluxo segue as etapas abaixo, desde a obtenção dos dados até a geração da sequência consenso.

---

## 🚀 Etapas do Fluxo

### 1. **Obtenção dos Dados** 📡
- **Fontes de Dados:** Os arquivos de sequenciamento das amostras são obtidos através do **BaseSpace da Illumina** no formato `.fastq`. 
- **Sequência de Referência:** A sequência de referência é baixada do **NCBI** em formato `.fasta`.

---

### 2. **Pré-processamento** 🛠️
- **Controle de Qualidade:** 
  - Utiliza-se a ferramenta **FASTP** para realizar o controle de qualidade das sequências.
  - Remove reads de baixa qualidade e realiza a **trimagem de bases**.
  - Gera relatórios detalhados de qualidade.
  
- **Indexação da Referência:**
  - A sequência de referência obtida do NCBI é indexada com o **BWA** (usando o comando `bwa index`), preparando-a para o alinhamento.

---

### 3. **Alinhamento** 🧬
- **Alinhamento das Amostras:** O alinhamento das sequências das amostras à referência é realizado utilizando **BWA MEM**.
  - Gera um arquivo `.SAM`, que é convertido para o formato binário `.BAM` com o comando `samtools view`.

---

### 4. **Indexação** 🔑
- **Organização e Indexação do BAM:**
  - O arquivo `.BAM` gerado é compactado, ordenado e indexado com a combinação dos comandos **Samtools sort** e **Samtools index**.
  - Isso garante que a sequência esteja organizada por **posição genômica**.

---

### 5. **Chamada de Variantes** 🔬
- **Detecção de Variantes:** O comando **Samtools mpileup** processa o arquivo `.BAM` indexado e gera um arquivo `.BCF`.
  - **Bcftools call** identifica variantes (SNPs, deleções, inserções), gerando o arquivo de variantes em formato `.VCF`.

---

### 6. **Consenso** 🧬
- **Geração da Sequência Consenso:**
  - O arquivo `.VCF` é indexado com **Bcftools index**.
  - A sequência consenso é gerada usando o comando **Bcftools consensus**, resultando em um arquivo `.fasta`.

---

## 🛠️ Ferramentas Utilizadas

- **BaseSpace (Illumina)**: Plataforma para obtenção de dados de sequenciamento.
- **NCBI**: Fonte para sequências de referência genômica.
- **FASTP**: Ferramenta para controle de qualidade e trimagem.
- **BWA**: Ferramenta de alinhamento de sequências.
- **Samtools**: Utilizado para manipulação de arquivos SAM/BAM/VCF.
- **Bcftools**: Ferramenta para chamada de variantes e geração de consenso.

---

## 📥 Como Executar

Para rodar o pipeline, basta seguir as instruções descritas no arquivo [installation_instructions.md](link_para_o_arquivo) ou consultar a documentação para detalhes sobre a configuração de ambiente e dependências.

---

🔗 **Contribuições:**  
Sinta-se à vontade para contribuir! Para mais informações, consulte o arquivo [CONTRIBUTING.md](link_para_o_arquivo).

📜 **Licença:**  
Este projeto está licenciado sob a [Licença MIT](link_para_o_arquivo).

---

🔍 **Contato:**  
Se tiver dúvidas ou sugestões, entre em contato pelo email: `contato@exemplo.com`

