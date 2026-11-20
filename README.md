# ONIBUS CI
## 1. Contextualização do Sistema

* Problema a ser resolvido: As linhas de ônibus de João Pessoa não oferecem tanta acessibilidade para deslocar-se ao CI (Centro de informatica), e muitas pessoas dependem desse meio de locomoção tanto para ir quanto para voltar da universidade. Porém, as opções de ônibus para o CI são muito escassas, localizadas em pontos isolados que podem ser um perigo com o passar do tempo.
* O mini-sistema, utilizara valores aproximados para estimar o horário tanto de chegada no ponto, quanto de saída do terminal, tendo em mente que as estimativas já são inconsistentes.
* Linhas disponiveis em questao: 203,207,304,307,508,9901.
* Ate 4 linhas poderão ser cadastradas, e o horário de saída do terminal deverá ter como referencia o horário disponível no site da semob https://servicos.semobjp.pb.gov.br/linhas-de-onibus/.

1. **Cadastro fixo de 4 linhas (`TAM = 4`):** Armazena número da linha, intervalo de saída do terminal (em minutos) e tempo de deslocamento até o ponto (em minutos).
2. **Validação de entradas (`do-while`):** Número da linha e intervalo devem ser maiores que `0`; deslocamento deve ser `>= 0`; escolha da linha entre `1` e `4`; hora entre `0` e `23` e minuto entre `0` e `59`.
3. **Cálculo de chegada e virada de dia:** Converte a hora atual em minutos, encontra a próxima saída do terminal (próximo múltiplo do intervalo), soma o deslocamento até o ponto e ajusta o horário final para o formato 24h (`% 24`).
4. **Alerta condicional (`if-else`):** Se o tempo de espera até o ponto for `<= 5` minutos, exibe alerta de chegada iminente; caso contrário, informa margem de tempo.
5. **Controle sem variáveis globais:** Variáveis da `main` são atualizadas exclusivamente por passagem por referência (`&` e `*`).



## 2. Funções

* **`void exibirMenu(void)`**
* **Entrada:** Nenhuma.
* **Processamento / Saída:** Imprime na tela as opções do menu principal (cadastrar linhas, consultar ônibus, exibir relatório e sair).


* **`void cadastrarLinhas(LinhaOnibus linhas[], int tamanho, int *qtdCadastradas)`**
* **Entrada:** `linhas[]` (referência ao vetor de structs), `tamanho` (valor `4`) e `qtdCadastradas` (referência/ponteiro para variável da `main`).
* **Processamento / Saída:** Lê e valida os dados das 4 linhas usando `for` e `do-while`, grava no vetor `linhas[]` e atualiza `*qtdCadastradas` na `main`.


* **`void consultarProximoOnibus(const LinhaOnibus linhas[], int tamanho, int qtdCadastradas, int *totalConsultas)`**
* **Entrada:** `linhas[]` (referência somente leitura), `tamanho` e `qtdCadastradas` (valor) e `totalConsultas` (referência/ponteiro).
* **Processamento / Saída:** Valida a linha escolhida e o horário atual, calcula o tempo de espera e a hora de chegada no ponto, exibe o resultado com alerta condicional (`if-else`) e incrementa `*totalConsultas` na `main`.


* **`void exibirRelatorio(const LinhaOnibus linhas[], int tamanho, int qtdCadastradas, int totalConsultas)`**
* **Entrada:** `linhas[]` (referência somente leitura), `tamanho`, `qtdCadastradas` e `totalConsultas` (valor).
* **Processamento / Saída:** Exibe o resumo de linhas cadastradas, total de consultas realizadas e os dados de cada uma das 4 linhas.


* **`int main(void)`**
* **Entrada:** Nenhuma.
* **Processamento / Saída:** Declara as variáveis locais de controle e executa o menu em loop `do-while` com `switch-case` até a opção `0` (sair), retornando `0`.
