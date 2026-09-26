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

1. Abrir o ambiente MATLAB (versão R2020a ou superior) com a *Fuzzy Logic Toolbox* instalada.
2. Executar o script principal através do comando:
   ```matlab
   run('fuzzy_mppt.m')
   ```

## Cálculos Manuais 

**O desenvolvimento das 5 fases do processo de Inferência Fuzzy, encontra-se no documento:** 


## Comparação de Resultados ($\Delta P = -1{,}0\text{ p.u.}$, $\Delta V = 0{,}25\text{ p.u.}$)

* **Cálculo Manual (Discretização $\Delta = 0{,}1\text{ p.u.}$)**: $\Delta D = -0{,}2181\text{ p.u.}$
* **Simulação Computacional (MATLAB `evalfis`)**: $\Delta D \approx -0{,}218\text{ p.u.}$
* **Análise Comparativa**: O valor obtido computacionalmente coincide com o cálculo manual analítico, apresentando variação residual insignificante decorrente da resolução contínua do integrador numérico do MATLAB face à discretização de 21 pontos do cálculo manual.

## Autoria
* **Aluno**: Andrey Alcântara da Silva Oliveira
* **Disciplina**: Automação Inteligente — IFBA
