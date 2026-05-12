1:Entradas e saídas do sistema Entradas

São os elementos que o sistema lê:

Botão de iniciar Tipo: digital (pressionado / não pressionado) Potenciômetro de tempo Tipo: analógico (0 a 1023) Potenciômetro de intensidade Tipo: analógico (0 a 1023) Saídas

São os elementos que o sistema controla:

LED vermelho → sistema parado LED amarelo → processo em execução LED verde → processo finalizado 3 LEDs de intensidade 1 LED → baixa 2 LEDs → média 3 LEDs → alta

2:Componentes do sistema e suas funções Microcontrolador (ex: Arduino) Executa toda a lógica do sistema Botão (push button) Permite iniciar o processo Potenciômetro de tempo Define a duração do ciclo (1 a 10 segundos) Potenciômetro de intensidade Define o nível do processo (baixo/médio/alto) LEDs Vermelho → estado parado Amarelo → em execução Verde → finalizado LEDs extras → indicam intensidade Resistores Protegem LEDs e garantem leitura correta do botão

3:Regras de funcionamento Estado inicial LED vermelho ligado Sistema aguardando botão Ao pressionar o botão Ler o potenciômetro de tempo Converter valor (0–1023 → 1–10 segundos) Ler potenciômetro de intensidade Determinar nível: 0–341 → baixa 342–682 → média 683–1023 → alta Salvar esses valores (não mudar durante execução) Durante execução LED vermelho desligado LED amarelo ligado LEDs de intensidade mostram nível definido Esperar tempo configurado Após término LED amarelo desligado LED verde ligado Após pequeno tempo (ou reset lógico): LED verde desliga LED vermelho liga novamente

4:1. Detectar botão pressionado if (botao == PRESSIONADO) { iniciarProcesso(); } 2. Converter intensidade if (valorIntensidade <= 341) { nivel = BAIXO; } else if (valorIntensidade <= 682) { nivel = MEDIO; } else { nivel = ALTO; } 3. Controlar LEDs de intensidade if (nivel == BAIXO) { liga1LED(); } else if (nivel == MEDIO) { liga2LEDs(); } else { liga3LEDs(); } 4. Estados do sistema

Uma variável de estado ajuda muito:

if (estado == PARADO) { ligaLEDVermelho(); } else if (estado == EXECUTANDO) { ligaLEDAmarelo(); } else if (estado == FINALIZADO) { ligaLEDVerde(); } 5. Controle do tempo if (tempoAtual - tempoInicio >= tempoConfigurado) { finalizarProcesso(); }
