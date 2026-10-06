# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<a href= "https://www.fiap.com.br/"><img src="assets/logo-fiap.png" alt="FIAP - Faculdade de Informática e Admnistração Paulista" border="0" width=40% height=40%></a>
</p>

<br>

# CardioIA – Fase 2: Diagnóstico Automatizado (IA no Estetoscópio Digital)

## Grupo 79

## 👨‍🎓 Integrante:
- Marlon Paulino Marinho – RM566793

## 👩‍🏫 Professores:
### Tutor(a)
- Leonardo Ruiz Orabona
### Coordenador(a)
- André Godoi Chiovato

## 🎥 Vídeo de demonstração  # TROCAR LINK , N ESQUECER APOS GRAVAR ################
[LINK DO VÍDEO]

## 📜 Descrição

Nesta fase do CardioIA, simulei um "estetoscópio digital": um módulo que lê textos de pacientes (inclusive algumas variações do português como gírias locais ou sinônimos, reconhece sintomas e sugere um diagnóstico ou um nível de risco. O projeto foi dividido em duas partes para melhor organização.

**Parte 1 – Extração de sintomas e diagnóstico (NLP baseado em regras)**

- `frases.txt`: 10 relatos de pacientes, cada um com o que a pessoa sente, quando começou e como isso afeta a rotina.
- `mapa_conhecimento.csv`: mapa que liga sintomas (Sintoma 1 e Sintoma 2) a três doenças: Infarto, Angina e Insuficiência Cardíaca.
- `sinonimos.csv`: dicionário com jeitos populares de falar o mesmo sintoma (ex.: "agonia no peito" → "dor no peito", "canseira" → "cansaço constante", "canela inchada" → "tornozelos inchados"). Paciente não fala como livro de medicina, então essa camada traduz a linguagem do dia a dia antes da busca.
- O código padroniza o texto (minúsculo e sem acento), troca os sinônimos, procura os sintomas do mapa e dá 1 ponto para cada doença encontrada. Vence a doença com mais pontos.
- Em caso de empate, o resultado aparece como "Inconclusivo" e o sistema sugere priorizar a doença mais grave (Infarto > Angina > Insuficiência Cardíaca), seguindo a lógica de triagem de pronto-socorro: na dúvida, trata como o caso mais sério.

Resultado: as 10 frases foram diagnosticadas, e frases novas escritas de forma popular também foram reconhecidas por causa dos sinônimos.

**Parte 2 – Classificador de risco (Machine Learning)**

- `frases_risco.csv`: 40 frases rotuladas (20 "alto risco" e 20 "baixo risco").
- As frases foram transformadas em números com **TF-IDF** e usadas para treinar uma **Regressão Logística** (Scikit-learn).
- Separação de 75% para treino (30 frases) e 25% para teste (10 frases), mantendo a proporção entre as classes.

Resultado: **acurácia de 90%** nas 10 frases de teste.

**Limitações e viés observados**

- O único erro foi na frase "dormi mal e acordei com sono" (baixo risco), classificada como alto risco. A palavra "acordei" apareceu no treino em "acordei sufocado", e o TF-IDF olha o peso das palavras, não o sentido da frase. Isso mostra como uma base pequena pode criar associações erradas.
- Com só 40 frases, a acurácia muda bastante dependendo de quais frases caem no teste. Em um sistema real, seria preciso uma base muito maior e revisada por profissionais de saúde.
- O mapa de conhecimento é simplificado: alguns sintomas, como falta de ar, aparecem em mais de uma doença na vida real. Este projeto é acadêmico e não substitui avaliação médica.
- Próxima evolução: tratar palavras de intensidade ("dor da peste", "dor forte") como um peso extra no risco, e não como sintoma.

## ✨ Extras (além do pedido no enunciado)

- **Dicionário de sinônimos populares** (`src/parte1/sinonimos.csv`): mais de 40 formas do dia a dia de descrever um sintoma ("agonia no peito", "canseira", "canela inchada", "sem coragem pra nada"), incluindo expressões regionais e erros comuns de escrita. O sistema traduz para o termo do mapa antes de buscar, sem precisar mexer no conhecimento médico.
- **Padronização do texto**: maiúsculas, minúsculas e acentos não atrapalham a busca ("Tórax" = "torax").
- **Desempate por gravidade**: quando duas doenças empatam, o resultado aparece como "Inconclusivo" e o sistema sugere priorizar a mais grave, como numa triagem de pronto-socorro.
- **Teste com linguagem popular**: o notebook da Parte 1 mostra frases novas, fora do mapa, sendo reconhecidas pelos sinônimos, além de um caso de empate.
- **Conferência frase a frase**: o notebook da Parte 2 mostra o que o modelo acertou e errou no teste, e o erro encontrado é analisado na seção de limitações.
- **Leitura direta do repositório**: os notebooks buscam os dados no próprio GitHub, então basta abrir no Colab e clicar em "Executar tudo", sem upload de arquivos.
- **Código comentado em linguagem simples**: cada etapa tem um título e comentários explicando o que faz.

## 📁 Estrutura de pastas

- **assets**: imagens do projeto.
- **config**, **scripts**, **document**: pastas do modelo FIAP (sem uso nesta fase).
- **src/parte1**:
  - `frases.txt` – 10 relatos de pacientes
  - `mapa_conhecimento.csv` – sintomas x doenças
  - `sinonimos.csv` – linguagem popular x termo do mapa
  - `parte1_extracao.ipynb` – código de extração e diagnóstico
- **src/parte2**:
  - `frases_risco.csv` – 40 frases rotuladas
  - `parte2_classificador.ipynb` – TF-IDF, treino e avaliação
- **README.md**: este arquivo.

## 🔧 Como executar o código

1. Abra o notebook desejado no GitHub e clique em **Open in Colab**.
2. No Colab, clique em **Ambiente de execução → Executar tudo**.
3. Não é preciso fazer upload de arquivos: os notebooks leem os dados direto deste repositório.

Bibliotecas usadas (já vêm instaladas no Google Colab): `pandas`, `unicodedata` e `scikit-learn`.

## 🤝 Apoio

Revisão com apoio de ferramenta de IA.

## 🗃 Histórico de lançamentos

- 0.1.0 - 06/10/2026
  - Fase 2: extração de sintomas (Parte 1) e classificador de risco (Parte 2).

## 📋 Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/agodoi/template">MODELO GIT FIAP</a> por <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://fiap.com.br">Fiap</a> está licenciado sobre <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">Attribution 4.0 International</a>.</p>


