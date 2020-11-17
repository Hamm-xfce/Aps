# Aps
import os
import time
os.system('cls')

def ordenarDados(dicionario,indice_analisado): # Função que ordena os dicionarios
    tamDict = len(dicionario)

    for i in range (tamDict - 1):
        menorValor = i

        for j in range(i, tamDict):
            if dicionario.get(j)[indice_analisado] < dicionario.get(menorValor)[indice_analisado]:
                menorValor = j
        
        if dicionario.get(i)[indice_analisado] > dicionario.get(menorValor)[indice_analisado]:

            dicionario[i], dicionario[menorValor] = dicionario[menorValor], dicionario[i]

def conversor(dicionario,index,tipo): #Função que converte os Tipos de dados definidos  
    if tipo == 1: 
        for i in dicionario:
            dicionario.get(i)[index] = float(dicionario.get(i)[index])
    elif tipo == 2:
        for i in dicionario:
            dicionario.get(i)[index] = str(dicionario.get(i)[index])
    else:
        return('Tipo de Arquivo não especificado')

def tipoIndex (indice): # Função que define Str ou Float.
    if (indice == 0) or ((indice >= 3) and (indice <=10)):
        return 1
    elif (indice == 1) or (indice == 2) or (indice == 11):
        return 2
    else:
        return exit('\n \n Valor de indice não encontrado! \n Digite um numero de 0 a 11 \n \n ') 
        
# Abre o Arquivo csv lê todas as suas linhas 
x = open("pokemon.csv")
linhas = x.readlines()
tam = len(linhas)

# cria um dicionario
dicionario = {}

#Preenche o dicionario com todas as linhas do aquivo 
for i in range(tam-1):
    dicionario[i] = linhas[i+1].replace('\n','').split(',')

# Menu de Seleção de Indices
indice = int(input('= Valores e seus respectivos indices = \n \n 0 = Número na PokeDex \n 1 = Nome do Pokemon \n 2 = Tipo \n 3 = Valor Total \n 4 = HP \n 5 = Ataque \n 6 = Defesa \n 7 = Ataque Especial \n 8 = Defesa Especial \n 9 = Velocidade \n 10 = Geração \n 11 = Lendarios \n \n Selecione o Indice que deseja ordenar : '))

print('\nOrdenando Indice...\n')
time.sleep(3)

#Chamada da Função que Define o tipo
tipo = tipoIndex(indice)

#Chamada da Função que converte os dados
conversor(dicionario,indice,tipo)

#Chamada da Função que ordena os dados
ordenarDados(dicionario,indice)

print('Criando Arquivo...\n')
time.sleep(3)

#Criação de um arquivo txt
saida_file = open('PokemonOrdenado.txt', 'w')
saida_file.write(linhas[0])

#Transfere os valores do dicionario em forma de texto pro arquivo txt criado
for key , value in dicionario.items():
    saida_file.write(str(value).replace('[','').replace(']','') + "\n")
print('Concluindo... \n')
time.sleep(3)
#fecha o arquivo
saida_file.close()
print('Arquivo Finalizado!\n')
