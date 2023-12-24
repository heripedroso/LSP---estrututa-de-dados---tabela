# LSP---estrututa-de-dados---tabela
Estrutura de dados do tipo TABELA

Geralmente iremos ver valores serem atribuídos à variáveis isoladamente:
```
nNumEmp = R034FUN.NumEmp;
nTipCol = R034FUN.TipCol;
nNumCad = R034FUN.NumCad;
```
No entanto, iremos sentir a necessidade de agruparmos esses valores em algo semelhante a um objeto do tipo DTO, tal como.
```
@==============================================================================@
Definir Tabela objColaborador[1] = {   
                                     Numero nNumEmp;
                                     Numero nTipCol;                                     
                                     Numero nNumCad; 
                                     Numero nNumCra;  
                                     Numero n2TNumCad;  @ Cadastro do 2º vínculo (2º teto), caso o colaborador seja da área assistencial (médico, enfermeiro, psicólogo, etc). @
                                     Numero n2TNumCra;  @ Crachá do 2º vínculo (2º teto), caso o colaborador seja da área assistencial (médico, enfermeiro, psicólogo, etc). @
                                   };             

@==============================================================================@
```
Os casos em que senti mais esta necessidade foram nos agrupamentos de valores de saída de alguma função, e que mais tarde poderiam também servir como entrada para outras funções.
```
@==============================================================================@
Definir Tabela objHorario[1] = {   
                                     Numero nCodHorario;
                                     Numero nCargaHorariaDiaria;                                     
                                     Numero nEhHorarioNoturno; 
                                     Numero nEhHorario24h;  
                                     Numero nToleranciaSaidaAntecipada;  
                                     Numero nToleranciaAtraso;
                                     Numero nHoraEntradaToleranciaAntes; @ Limite que define a partir de que momento uma marcação se torna válida. Por exemplo: marcações de ponto que são registradas muito cedo não são consideradas válidas. @
                                     Numero nHoraSaidaToleranciaApos;  @ Limite que define até em que momento uma marcação se torna válida. Por exemplo: marcações de ponto que são registradas muito tarde não são consideradas válidas. @
                                     Numero nHoraMetadeDoPeriodo; @ Variável de referência para definir se uma marcação é de entrada ou de saída. Para os horários norturno e de 24h, a virada do dia é a referência. @
                               };             

@==============================================================================@
```



```
@==============================================================================@
Definir Tabela tabSituacoesMes[4] = {   
                                     Numero nQtdeFaltasDiurnas;
                                     Numero nQtdeFaltasNoturnas;                                     
                                     Numero nQtdeSuspensoes; 
                                     Numero nQtdeAdvertencias;  
                                     Numero nQtdeOutrosAfastamentos;  };             

@==============================================================================@
Definir Funcao ZeraTabSituacoesMes();

Funcao ZeraTabSituacoesMes();
{ 
   nContador = 1;
   ENQUANTO(nContador <= 4) 
   {         
      tabSituacoesMes[nContador].nQtdeFaltasDiurnas = 0;
      tabSituacoesMes[nContador].nQtdeFaltasNoturnas = 0;  
      tabSituacoesMes[nContador].nQtdeSuspensoes = 0;
      tabSituacoesMes[nContador].nQtdeAdvertencias = 0;
      tabSituacoesMes[nContador].nQtdeOutrosAfastamentos = 0;  

      nContador =  nContador + 1;  
   }; 

};
@==============================================================================@
```

## Recomendações
Para usar a função/estrutura de dados na regra, deve-se declará-la no início da mesma.
É interessante que se reserve, por exemplo, a regra 001 apenas para implementar funções.

Em implementações de relatório, tenho o hábito de declarar as funções em Funções Globais no Modelo Gerador.

![image](https://github.com/heripedroso/LSP---converte-minutos-em-HH-MI/assets/22459829/fa6ef8f7-399d-4923-9c2e-a814f502bddc)
