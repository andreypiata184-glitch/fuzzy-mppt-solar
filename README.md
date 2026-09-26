# Controle Fuzzy MPPT para Rastreamento do Ponto de Máxima Potência - Projeto, Cálculo Manual e Implementação Computacional de um Sistema de Inferência Fuzzy para energia Solar Fotovoltaica

Sistema de inferência fuzzy baseado no método de Mamdani para ajuste contínuo do ciclo de funcionamento (*duty cycle*) de conversores CC-CC em arranjos fotovoltaicos.

## Variáveis do Sistema

* **Entrada 1 - Variação de Potência ($\Delta P$)**: Universo $[-1{,}0; 1{,}0]\text{ p.u.}$, termos: `{Negativa, Zero, Positiva}`.
* **Entrada 2 - Variação de Tensão ($\Delta V$)**: Universo $[-1{,}0; 1{,}0]\text{ p.u.}$, termos: `{Negativa, Zero, Positiva}`.
* **Saída - Variação do Duty Cycle ($\Delta D$)**: Universo $[-1{,}0; 1{,}0]\text{ p.u.}$, termos: `{Diminuir, Manter, Aumentar}`.

## Base de Regras

| $\Delta P$ \ $\Delta V$ | Negativa | Zero | Positiva |
| :--- | :---: | :---: | :---: |
| **Negativa** | Aumentar | Manter | Diminuir |
| **Zero** | Diminuir | Manter | Aumentar |
| **Positiva** | Aumentar | Manter | Diminuir |

## Instruções de Execução

1. Abra o arquivo [fuzzy_solar.m](fuzzy_solar.m) no ambiente MATLAB com a *Fuzzy Logic Toolbox* instalada.
2. Executar o script principal.
3. O terminal exibirá os resultados obtidos.
4. Uma janela gráfica plotará a região do Centro de Área (CDA).

## Resultado da Simulação 
Para o instante de amostragem avaliado, o sistema registrou uma queda extrema de potência ($\Delta P = -1{,}0$ p.u.) associada a um aumento de tensão ($\Delta V = 0{,}25$ p.u.). Pela lógica da técnica *Perturbe e Observe* mapeada na base de regras, o controlador ativou simultaneamente as diretrizes de manutenção e decremento da variável de controle.

Através do processo de inferência de **Mamdani**, a agregação das contribuições gerou uma região fuzzy de saída concentrada no semiplano negativo. A conversão desta área para um valor acionável, utilizando o método de defuzzificação por **Centro de Área (CDA)**, produziu o sinal *crisp* exato de $\Delta D = -0{,}2181$ p.u.

<img width="640" height="142" alt="resultado_matlab" src="https://github.com/user-attachments/assets/81f761ba-5a21-4cea-a566-7841384c1cc2" />


<img width="888" height="322" alt="grafico_cda" src="https://github.com/user-attachments/assets/e367d4bb-269b-49e6-bdc1-05afe85a0ad8" />



## Cálculos Manuais 

**O desenvolvimento das 5 fases do processo de Inferência Fuzzy, encontra-se no documento:** [Cálculo Manual Analítico](Arquivos/calculo_manual.pdf).


## Comparação de Resultados ($\Delta P = -1{,}0\text{ p.u.}$, $\Delta V = 0{,}25\text{ p.u.}$)

* **Cálculo Manual (Discretização $\Delta = 0{,}1\text{ p.u.}$)**: $\Delta D = -0{,}2181\text{ p.u.}$
* **Simulação Computacional (MATLAB `evalfis`)**: $\Delta D \approx -0{,}218\text{ p.u.}$
* **Análise Comparativa**: O valor obtido computacionalmente coincide com o cálculo manual analítico, apresentando variação residual insignificante decorrente da resolução contínua do integrador numérico do MATLAB face à discretização de 21 pontos do cálculo manual.

## Conclusão e Validação do Modelo Matemático

A análise comparativa entre a modelagem algébrica e a simulação computacional demonstra uma convergência estrutural rigorosa. O **cálculo manual**, fundamentado na discretização do universo de discurso com passo $\Delta = 0{,}1$ p.u., resultou em uma defuzzificação por **Centro de Área (CDA)** de $\Delta D = -0{,}2181$ p.u. 

Por sua vez, o **algoritmo computacional** processou as matrizes de inferência de **Mamdani** gerando um valor perfeitamente análogo. O diminuto desvio residual observado (na casa dos milésimos) não configura um erro de modelagem, mas reflete estritamente a diferença de **resolução numérica** do integrador. Enquanto o método analítico manual empregou uma soma de Riemann com 21 pontos amostrais, a arquitetura do *software* opera com uma malha de discretização contínua e substancialmente mais fina.

Portanto, atesta-se que a lógica de controle foi fielmente mapeada para o domínio fuzzy. A simulação computacional validou a exatidão do equacionamento matemático, provando que o controlador possui robustez para atuar fisicamente de forma determinística e estável na busca contínua pelo **Ponto de Máxima Potência (MPP)** do arranjo fotovoltaico.


## Autoria
* **Aluno**: Andrey Alcântara da Silva Oliveira
* **Disciplina**: Automação Inteligente — IFBA
