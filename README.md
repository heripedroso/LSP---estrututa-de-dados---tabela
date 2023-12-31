# LSP---estrututa-de-dados---tabela
Estrutura de dados do tipo TABELA

## Por que usar tabela para agrupar valores?
Geralmente iremos ver valores serem atribuídos à variáveis isoladamente:
```
nNumEmp = R034FUN.NumEmp;
nTipCol = R034FUN.TipCol;
nNumCad = R034FUN.NumCad;
```
No entanto, iremos sentir a necessidade de agruparmos esses valores em algo semelhante a um objeto do tipo DTO, tal como:
```
/*
A posição 02 armazena as informações do 2º teto, caso o colaborador tenha. Para os profissionais da saúde, é permitido possuir mais de um vínculo desde que em horário diferentes.
*/
Definir Tabela objColaborador[2] = {   
                                     Numero nNumCPF;
                                     Numero nNumEmp;
                                     Numero nTipCol;                                     
                                     Numero nNumCad; 
                                     Numero nNumCra;
                                     Alfa aNome;
                                     Alfa aCargo;
                                     Alfa aCodCargo;
                                     Alfa aVinculo;
                                     Alfa aEscala;
                                     Alfa aFuncao;
                                     Alfa aCodFuncao;
                                     Alfa aLocal;
                                     Numero nNumSead;
                                     Numero nVinculoSead;
                                   };

objColaborador[1].nNumCPF = R034FUN.NumCpf;
objColaborador[1].nNumEmp = R034FUN.NumEmp;
objColaborador[1].nTipCol = R034FUN.TipCol;  
objColaborador[1].nNumCad = R034FUN.NumCad;
objColaborador[1].nNumCra = R034FUN.NumCra;

/*
Preenche a posição 2 se houver 2º vínculo
objColaborador[2].nNumEmp = 0;
objColaborador[2].nTipCol = 0;
objColaborador[2].nNumCad = 0;
objColaborador[2].nNumCra = 0;
*/


```
Os casos em que senti mais esta necessidade foram nos agrupamentos de valores de saída de alguma função, e que mais tarde poderiam também servir como entrada para outras funções.
```
Definir Tabela objHorario[1] = {   
                                     Numero nCodHorario;
                                     Numero nHoraEntrada;
                                     Numero nHoraSaida;
                                     Numero nCargaHorariaDiaria;                       
                                     Numero nEhHorarioNoturno; @ Valor booleano: 0 - horário diurno, 1 - horário noturno @
                                     Numero nEhHorario24h; @ Valor booleano: 0 - não é um horário de 24h, 1 - é um horário de 24h (plantão) @                                        
                                     Numero nToleranciaAtraso;
                                     Numero nToleranciaSaidaAntecipada;
                                     Numero nHoraEntradaToleranciaAntes; @ Limite que define a partir de que momento uma marcação se torna válida. Por exemplo: marcações de ponto que são registradas muito cedo não são consideradas válidas. @
                                     Numero nHoraSaidaToleranciaApos;  @ Limite que define até em que momento uma marcação se torna válida. Por exemplo: marcações de ponto que são registradas muito tarde não são consideradas válidas. @
                                     Numero nHoraMetadeDoPeriodo; @ Variável de referência para definir se uma marcação é de entrada ou de saída. Para os horários norturno e de 24h, a virada do dia é a referência. @
                               };


Definir Funcao retornaCargaHorariaETurno(Numero nCodHorario);

Funcao retornaCargaHorariaETurno(Numero nCodHorario);
{ 
    /*
     Utiliza cursor e variáveis de apoio para acessar o banco de dados.
    */

    objHorario[1].nCodHorario = nCodHorario;
    objHorario[1].nHoraEntrada = nHoraEntrada; 
    objHorario[1].nHoraSaida = nHoraSaida;
    objHorario[1].nCargaHorariaDiaria = nCargaHorariaDiaria;
    objHorario[1].nEhHorarioNoturno = nEhHorarioNoturno;
    objHorario[1].nEhHorario24h = nEhHorario24h;
    objHorario[1].nToleranciaAtraso = nToleranciaAtraso;
    objHorario[1].nToleranciaSaidaAntecipada = nToleranciaSaidaAntecipada;
    objHorario[1].nHoraEntradaToleranciaAntes = nHoraEntradaToleranciaAntes;
    objHorario[1].nHoraSaidaToleranciaApos = nHoraSaidaToleranciaApos;
    objHorario[1].nHoraMetadeDoPeriodo = nHoraMetadeDoPeriodo;
}


```
## Exemplo de uso como parâmetro de entrada em funções.
Se usarmos estes agrupamentos em chamadas de funções, o código se torna bem mais limpo e intuitivo.


```
Definir Funcao verificaSeHouveFalta();

Funcao verificaSeHouveFalta(){

     @ Carrega as variáveis de entrada. @
     nNumEmp = objColaborador[1].nNumEmp;
     nTipCol = objColaborador[1].nTipCol;  
     nNumCad = objColaborador[1].nNumCad;
     nNumCra = objColaborador[1].nNumCra;

     nCodHorario= objHorario[1].nCodHorario;
     nHoraEntrada = objHorario[1].nHoraEntrada; 
     nHoraSaida = objHorario[1].nHoraSaida;
     nCargaHorariaDiaria = objHorario[1].nCargaHorariaDiaria;
     nEhHorarioNoturno = objHorario[1].nEhHorarioNoturno;
     nEhHorario24h = objHorario[1].nEhHorario24h;
     nToleranciaAtraso = objHorario[1].nToleranciaAtraso;
     nToleranciaSaidaAntecipada = objHorario[1].nToleranciaSaidaAntecipada;
     nHoraEntradaToleranciaAntes = objHorario[1].nHoraEntradaToleranciaAntes;
     nHoraSaidaToleranciaApos = objHorario[1].nHoraSaidaToleranciaApos;
     nHoraMetadeDoPeriodo = objHorario[1].nHoraMetadeDoPeriodo;

     /*
          Restante da regra aqui.
     */

}
```

Por sua vez, a função verificaSeHouveFalta poderia armazenar os cálculos em outro agrupamento.
```
Definir Tabela objMarcacoesApuradas[1] = {   
                                     Numero nHouveFalta; @ Valor booleano: 0 - não houve falta, 1 - Houve falta @
                                     Numero nPrimeiraMarcacaoEntradaValida; @ Marcação de entrada válida. @  
                                     Numero nUltimaMarcacaoSaidaValida; @ Marcação de saída válida. @
                                   };   
```

## Recomendações
Para usar a função/estrutura de dados na regra, deve-se declará-la no início da mesma.
É interessante que se reserve, por exemplo, a regra 001 apenas para implementar funções.

Em implementações de relatório, tenho o hábito de declarar as funções em Funções Globais no Modelo Gerador.

![image](https://github.com/heripedroso/LSP---converte-minutos-em-HH-MI/assets/22459829/fa6ef8f7-399d-4923-9c2e-a814f502bddc)
