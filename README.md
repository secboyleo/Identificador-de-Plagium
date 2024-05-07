# Introducao-a-Ciencia-da-Computacao-Python-1
Projeto realizado para a conclusão do curso de introdução a Ciência da Computação com Python na Coursera

# COH-PYAH
```
import re
import math

def quantidade_total_caracteres(conjuntos):
    # retorna a quantidade de caracteres de um conjunto de palavras / frase / sentença
    quantidadeCaracteres = 0

    for conjunto in conjuntos:
        quantidadeCaracteres += len(conjunto)

    return quantidadeCaracteres


def tamanho_medio_palavras(palavras):
    #retorna a quantidade de caracteres dentro de uma palavra
    return (quantidade_total_caracteres(palavras) / len(palavras))


def le_assinatura():
    '''A funcao le os valores dos tracos linguisticos do modelo e devolve uma assinatura a ser comparada com os textos fornecidos'''
    print("Bem-vindo ao detector automático de COH-PIAH.")
    print("Informe a assinatura típica de um aluno infectado:")

    wal = float(input("Entre o tamanho médio de palavra:"))
    ttr = float(input("Entre a relação Type-Token:"))
    hlr = float(input("Entre a Razão Hapax Legomana:"))
    sal = float(input("Entre o tamanho médio de sentença:"))
    sac = float(input("Entre a complexidade média da sentença:"))
    pal = float(input("Entre o tamanho medio de frase:"))

    return [wal, ttr, hlr, sal, sac, pal]

def le_textos():
    '''A funcao le todos os textos a serem comparados e devolve uma lista contendo cada texto como um elemento'''
    i = 1
    textos = []
    texto = input("Digite o texto " + str(i) +" (aperte enter para sair):")
    while texto:
        textos.append(texto)
        i += 1
        texto = input("Digite o texto " + str(i) +" (aperte enter para sair):")

    return textos

def separa_sentencas(texto):
    '''A funcao recebe um texto e devolve uma lista das sentencas dentro do texto'''
    sentencas = re.split(r'[.!?]+', texto)
    if sentencas[-1] == '':
        del sentencas[-1]
    return sentencas

def separa_frases(sentenca):
    '''A funcao recebe uma sentenca e devolve uma lista das frases dentro da sentenca'''
    return re.split(r'[,:;]+', sentenca)

def separa_palavras(frase):
    '''A funcao recebe uma frase e devolve uma lista das palavras dentro da frase'''
    return frase.split()

def n_palavras_unicas(lista_palavras):
    '''Essa funcao recebe uma lista de palavras e devolve o numero de palavras que aparecem uma unica vez'''
    freq = dict()
    unicas = 0
    for palavra in lista_palavras:
        p = palavra.lower()
        if p in freq:
            if freq[p] == 1:
                unicas -= 1
            freq[p] += 1
        else:
            freq[p] = 1
            unicas += 1

    return unicas

def n_palavras_diferentes(lista_palavras):
    '''Essa funcao recebe uma lista de palavras e devolve o numero de palavras diferentes utilizadas'''
    freq = dict()
    for palavra in lista_palavras:
        p = palavra.lower()
        if p in freq:
            freq[p] += 1
        else:
            freq[p] = 1

    return len(freq)

def compara_assinatura(as_a, as_b):
    '''IMPLEMENTAR. Essa funcao recebe duas assinaturas de texto e deve devolver o grau de similaridade nas assinaturas.'''
    # mostra a similaridade das assinaturas
    soma = 0

    for i in range(0, 6):
        soma += math.fabs(as_a[i] - as_b[i])
    
    soma = soma / 6
    return round(soma, 2)

def calcula_assinatura(texto):
    '''IMPLEMENTAR. Essa funcao recebe um texto e deve devolver a assinatura do texto.'''
    frases = []
    palavras = []

    # separa as sentenças do texto
    sentencas = separa_sentencas(texto)

    # separa as frases do texto
    for sentenca in sentencas:
        frases += separa_sentencas(sentenca)

    # separa as palavras do texto
    for frase in frases:
        palavras += separa_palavras(frase)
    
    # define os traços linguisticos
    wal = tamanho_medio_palavras(palavras)
    ttr = n_palavras_diferentes(palavras) / len(palavras)
    hlr = n_palavras_unicas(palavras) / len(palavras)
    sal = quantidade_total_caracteres(sentencas) / len(sentencas)
    sac = len(frases) / len(sentencas)
    pal = quantidade_total_caracteres(frases) / len(frases)

    return [wal, ttr, hlr, sal, sac, pal]

def avalia_textos(textos, ass_cp):
    '''IMPLEMENTAR. Essa funcao recebe uma lista de textos e uma assinatura ass_cp e deve devolver o numero (1 a n) do texto com maior probabilidade de ter sido infectado por COH-PIAH.'''

    comparacoes = []

    for texto in textos:
        assinatura = calcula_assinatura(texto)
        comparacao = compara_assinatura(assinatura, ass_cp)
        comparacoes.append(comparacao)
    
    menor_comparacao = min(comparacoes)
    indice_menor_comparacao = (comparacoes.index(menor_comparacao) + 1)
    print(f"o autor do texto {indice_menor_comparacao} está infectado com COH_PYAH")

    return indice_menor_comparacao

# função de entrada do programa
def main():
    # solicita ao user a assinatura padrao
    ass_cp = le_assinatura()

    # solicita textos a serem comparados
    textos = le_textos()
    
    # faz a avaliação
    avalia_textos(textos, le_assinatura())

main()
```
