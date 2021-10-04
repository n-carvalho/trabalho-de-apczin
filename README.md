# trabalho-de-apczin

# A variável abaixo guarda o nome de cada coluna 
# como refererência

COLUNAS = [
    "id", 
    "education", 
    "income", 
    "income_work",
    "income_rent", 
    "income_capital", 
    "race", 
    "gender", 
    "weight",
]

# Implemente a função ler_linha, que recebe uma linha como string e
# retorna um valor do tipo que você escolher para representar 
# cada indivíduo.
def ler_linha(linha: str):
    celulas = linha.split(',')
    if(celulas[1] == ''):
        education = 0
    else:
        education = int(float(celulas[1]))
    if(celulas[2] == ''):
        income = 0
    else:
        income = int(float(celulas[2]))
    if(celulas[3] == ''):
        income_work = 0
    else:
        income_work = int(float(celulas[3]))
    if(celulas[4] == ''): 
        income_rent = 0
    else:
        income_rent = int(float(celulas[4]))
    if(celulas[5] == ''):
        income_capital = 0
    else:
        income_capital = (int(float(celulas[5])))
    if(celulas[6] == ''):
        race = 0
    else:
        race = int(celulas[6])
    if(celulas[7] == ''):
        gender = 0
    else:
        gender = int(celulas[7])
    if(celulas[8] == ''):
        weight = 0
    else:
        weight = int(float(celulas[8]))
    return (education, income, income_work, income_rent, income_capital, race, gender, weight)


#  Main
arquivo = open('pnad2012.csv')
colunas = arquivo.readline()
print('Colunas:', colunas)
pessoas = []
for linhas in arquivo:
    pessoas.append(ler_linha(linhas))

total_cod_1 = 0
total_cod_2 = 0
total_cod_outros = 0

for pessoa in pessoas:
    cod_genero = pessoa[6]  # extraia o gênero da pessoa (coluna gender)
    peso       = pessoa[7] # extraia o peso estatístico (coluna weight)
    
    if cod_genero == 1:
        total_cod_1 += peso
    elif cod_genero == 2:
        total_cod_2 += peso
    # Colocamos o else para ter certeza que os únicos
    # códigos existentes são 1 ou 2.
    else:
        total_cod_outros += peso
        
print('Códigos de gênero:')
print(f'  1: {total_cod_1:12_}')
print(f'  2: {total_cod_2:12_}')
print(f'  outros: {total_cod_outros:12_}')

MULHER = 2 # Complete com o código correto!
HOMEM  = 1

salario_homens = 0
salario_mulheres = 0
n_homens = 0
n_mulheres = 0

for pessoa in pessoas:
    salario = pessoa[2]  # extraia o valor na coluna income_work
    genero  = pessoa[6]  # extraia o gênero da pessoa (coluna gender)
    peso    = pessoa[7]  # extraia o peso estatístico (coluna weight)
    
    if genero == MULHER:
        salario_mulheres += salario * peso
        n_mulheres += peso
    
    if genero == HOMEM:
        salario_homens += salario * peso
        n_homens += peso
        

# O salário médio é o total dos salários dividido
# pelo total de pessoas.
salario_homens /= n_homens 
salario_mulheres /= n_mulheres 
razao = salario_mulheres / salario_homens

print('Salário médio:')
print(f'  homens: {salario_homens:.1f}')
print(f'  mulheres: {salario_mulheres:.1f}')
print(f'  relativo: {100 * razao:.0f}%')

salario_homens = 0
salario_mulheres = 0
n_homens = 0
n_mulheres = 0

for pessoa in pessoas:
    salario = pessoa[2]  # extraia o valor na coluna income_work
    genero  = pessoa[6]  # extraia o gênero da pessoa (coluna gender)
    peso    = pessoa[7]  # extraia o peso estatístico (coluna weight)
    
    if salario > 0:
        if genero == MULHER:
            salario_mulheres += salario * peso
            n_mulheres += peso
        
        if genero == HOMEM:
            salario_homens += salario * peso
            n_homens += peso
        

# O salário médio é o total dos salários dividido
# pelo total de pessoas.
salario_homens /= n_homens 
salario_mulheres /= n_mulheres 
razao = salario_mulheres / salario_homens

print('Salário médio:')
print(f'  homens: {salario_homens:.1f}')
print(f'  mulheres: {salario_mulheres:.1f}')
print(f'  relativo: {100 * razao:.0f}%')

# Pergunta a escolaridade para o usuário
escolaridade = int(input("Escolaridade (anos): "))


# (copie e cole o código da célula anterior e altere para incluir apenas a faixa
#  de escolaridade desejada)

edu_homens   = 0
edu_mulheres = 0
n_homens   = 0
n_mulheres = 0

for pessoa in pessoas:
    # Extraia as informações da pessoa
    escolaridade = pessoa[0]
    genero       = pessoa[6]
    peso         = pessoa[7]
    
    if genero == MULHER:
        edu_mulheres += escolaridade * peso
        n_mulheres += peso

    if genero == HOMEM:
        edu_homens += escolaridade * peso
        n_homens += peso
        

print('Escolaridade média:')
print(f'  homens: {edu_homens / n_homens:.1f}')
print(f'  mulheres: {edu_mulheres / n_mulheres:.1f}')

# Inicializamos cada categoria com a contagem parcial
# Lembramos que as raças são representadas por potências de
# dois
n_pessoas = {0: 0, 1: 0, 2: 0, 4: 0, 8: 0, 16: 0}

for pessoa in pessoas:
    # Complete o código para ler as informações sobre a pessoa
    raca = pessoa[5]
    peso = pessoa[7]
    
    # Aqui incrementamos o campo associado à raça da pessoa escolhida 
    n_pessoas[raca] += peso    
        

print('Distribução das raças:')
for raca_cod, n in n_pessoas.items():
    print(f'  {raca_cod:2.0f}: {n:12_}')

n_pessoas = {1: 0, 2: 0, 4: 0, 8: 0, 16: 0}
salarios = {1: 0, 2: 0, 4: 0, 8: 0, 16: 0}

for pessoa in pessoas:
    # Leia informações sobre a pessoa
    raca = pessoa[5]
    peso = pessoa[7]
    salario = pessoa[2]

    if salario > 0:
        # Atualize os acumuladores, somente para assalariados
        n_pessoas[raca] += peso
        salarios[raca] += salario * peso

print('Distribução de salários entre as raças:')
for raca, n in n_pessoas.items():
    media = salarios[raca] / n
    
    print(f'{raca:2.0f}: {media:.1f}')


RACA_BRANCO   = 16
RACA_PRETO    = 2
RACA_PARDO    = 4
RACA_INDIGENA = 8
RACA_AMARELO  = 1

# O 
RACA_NOMES = {
    0: 0,
    RACA_BRANCO: "branco",
    RACA_PRETO: "preto",
    RACA_PARDO: "pardo",
    RACA_INDIGENA: "indígena",
    RACA_AMARELO: "amarelo",
}

n_pessoas = {0: 0,1: 0, 2: 0, 4: 0, 8: 0, 16: 0}
escolaridades = {0: 0, 1: 0, 2: 0, 4: 0, 8: 0, 16: 0}

for pessoa in pessoas:
    # Leia informações sobre a pessoa
    raca = pessoa[5]
    peso = pessoa[7]
    escolaridade = pessoa[0]

    # Atualize os acumuladores n_pessoas e escolaridades
    
    n_pessoas[raca] += peso
    escolaridades[raca] += escolaridade * peso

print('Distribução de escolaridade entre as raças:')
for raca, n in n_pessoas.items():
    media = escolaridades[raca] / n
    raca = RACA_NOMES[raca]
    if(raca == 0):
        None
    else:
        print(f'  {raca}: {media:.1f}')

n_pessoas     = {k: [0] * 16 for k in [1, 2, 4, 8, 16]}
salarios      = {k: [0] * 16 for k in [1, 2, 4, 8, 16]}

for pessoa in pessoas:
    # Extraia informações sobre a pessoa    
    raca = pessoa[5]
    peso = pessoa[7]
    salario = pessoa[2]
    escolaridade = pessoa[0]

    if salario > 0:
        n_pessoas[raca][escolaridade] += peso    
        salarios[raca][escolaridade] += salario * peso

print('Distribução de salários entre as raças:')
for raca, n in n_pessoas.items():
    raca_nome = RACA_NOMES[raca]
    
    # Calculamos os salarios médios usando uma compreensão de listas
    #  - zip(as, bs), cria uma lista de pares (a, b)
    salarios_medios = [x / (y+0.01) for (x, y) in zip(salarios[raca], n)] 
    
    print(f'  {raca}: {salarios_medios}')

escolaridades = [0] * 16

for pessoa in pessoas:
    peso         = pessoa[7]
    escolaridade = pessoa[0]
    salario      = pessoa[2]

    # Selecionamos apenas os assalariados
    if salario > 0:
        escolaridades[escolaridade] += peso    

# Somamos as frações em cada escolaridade para obter a população total 
populacao = sum(escolaridades)

# Criamos pesos com as proporções da população em cada faixa de escolaridade
ws = [x / populacao for x in escolaridades]

print(ws)

salario = 0

for raca, rendas in salarios.items():
    for i in range(len(rendas)):
        salario += (rendas[i] * ws[i])/ n_pessoas[raca][i]
    raca = RACA_NOMES[raca]
    print(f'  {raca}: {salario}')
