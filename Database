import os #importei o os para poder remover os dados do cliente caso ele queira.
from datetime import datetime #importei o data time para poder colocar horário no extrato.
from time import strftime #importei esse strftime para poder colocar horário no extrato.
func = 10
#func = 10 é apenas um número aleatório maior que o pedido para que o while rode perfeitamente.

#Função para a criação do novo cliente, coloquei todas as variáveis em uma única linha lá na linha do IF, pois usei .split() no final. Obs.: coloquei os parametros com os dados para ficar mais fácil a manipulação.
def novo_cliente(nome, cpf, tipo_conta, valor_inicial, senha):
    novo_txt = open("Cliente" + cpf +".txt", "w") #abri um arquivo para criar a área com os dados do cliente, está como w pois, quando ele debitar, depositar, vai ter que mudar os dados que estão dentro do arquivo.
    novo_txt.write("Nome do cliente: "+ nome) #este .write está no indice 0, como o nome do cliente.
    novo_txt.write("\nTipo da conta: "+ tipo_conta) #este .write está no indice 1, com o tipo da conta do cliente.
    valor_inicial = str(valor_inicial) #aqui eu tive que transferir o valor_inicial que estava como float (pois no debito de algum modo, ele só aceita float) para str para poder printar no .write dos dados do cliente.
    novo_txt.write("\nValor inicial da conta: "+ valor_inicial) #este .write está no indice 2 e serve para colocar o valor inicial da conta do cliente.
    novo_txt.write("\nSenha do cliente: "+ senha) #Este .write está no indce 3 e serve para colocar a senha do cliente.
    #todos tem \n que serve para poder pular linha
    novo_txt.close() #aqui eu fechei o arquivo
    print() #coloquei print vazio para pular linha
    print() #coloquei print vazio para pular linha
    print("***Conta criada com sucesso!***") #print falando que a conta foi criada com sucesso.

    #arquivo novo para quando for abrir o extrato lá embaixo já estar com os dados salvos.
    novo_txt = open(cpf +".txt", "a") #Abri um arquivo apenas com o cpf, diferente do primeiro que contém 'Cliente', para diferenciar extrato dos dados do cliente.
    novo_txt.write("Nome:" + nome + "\n") # Este .write serve para colocar o nome do cliente, como no arquivo novo_txt acima, porém este servirá para postar o extrato do cliente.
    novo_txt.write("CPF:" + cpf + "\n") #Este .write serve para colocar o CPF do cliente.              
    novo_txt.write("Conta:" + tipo_conta + "\n") #Este .write serve para colocar o tipo de conta do cliente
    #coloquei \n neles, para que possam pular linha.
    #não coloquei senha pois no extrato do Exemplo do professor não havia, logo também não adicionei senha.
    data = datetime.now() #função para criar o horário, foi importado lá nas linhas 2 e 3
    #esse tipo de data, foi o que pesquisei na internet, para ficar mais fácil a exibição da hora.
    data = data.strftime("%d/%m/%Y %H:%M") #Função que mostra dia mes ano hora e minuto
    data = str(data) #tive que transformar data para str.
    #primeiro histórico do extrato.
    #Jeito de ficar salvo pego do print do professor como exemplo para ser feito.
    valor_inicial = float(valor_inicial) #aqui diferentemente de lá em cima, voltei o valor inicial para float, pois se não, ele não printava certo :(
    print() #coloquei print vazio para pular linha
    print() #coloquei print vazio para pular linha
    novo_txt.write("%s    +    %.2f     Tarifa: 0.00 Saldo:       %.2f  \n" %  (data, valor_inicial, valor_inicial)) #Este .write serve para imprimir os dados igual o do exemplo do professor, mas com as mudanças necessárias usando o %
    novo_txt.close()#aqui eu fechei o arquivo
    
#Função para apagar os dados do cliente
def Apaga_Cliente():
    cpf = input("Digite o seu CPF: ") #Pedi o cpf do cliente. Obs.: Essa foi a única função que pedi os dados aqui dentro do input, pois só havia CPF, então não achei necessidade de colocar no IF
    if cpf in open(cpf + ".txt", 'r').readlines()[1]: #Se o cpf digitado estiver cadastrado, ele deletará todos os dados.
        os.remove(cpf + ".txt")#Aqui ele irá remover o arquivo do extrato
        os.remove("Cliente" + cpf +".txt")#Aqui ele irá remover o arquivo dos dados do cliente
        print("***Dados deletados com sucesso!***")#Printará dados deletados com sucesso

#Função para debitar da conta do cliente, parametros para poder fazer as mudanças necessárias.
def Debita(cpf, senha, valor_debito):
        #abri em modo leitura para poder fazer um for com essa leitura e a criação da lista para colocar tudo que está dentro do 'novo_txt' na lista e posteriormente no for.
        novo_txt = open("Cliente" + cpf +".txt", 'r')
        lista = novo_txt.readlines() #salvei a tudo que está no arquivo novo_txt em uma variável, para poder usa-lá num for posteriormente.
        novo_txt.close()#fechei o arquivo.
        guardarvalor = "" #Aqui serve para guardar o valor que será achado posteriormente.
        guardarsenha = "" #Aqui serve para guardar a senha que será achada posteriormente.
        for x in range(len(lista)): #ele vai procurar o que está dentro da lista
            #se o 'Valor' estiver na lista, ele vai guardar o valor na lista[x].
            if "Valor" in lista[x]:
                guardarvalor = lista[x]
            #se o 'Senha' estiver na lista, ele vai guardar a senha na lista[x].    
            if "Senha" in lista[x]:
                guardarsenha = lista[x]
        #saldo é para guardar em valores separados e pegar sempre o último elemento        
        saldo = guardarvalor.split(' ')[-1]
        #saldosenha é para guardar em valores separados e pegar sempre o último elemento     
        saldosenha = guardarsenha.split(' ')[-1]
        #função para ver se a senha digitada pelo usuário é igual a senha da conta do cliente, se for vai rodar tudo perfeitamente para poder ocorrer o débito.
        if senha == saldosenha: #se a senha digitada for a mesma da que o cliente cadastrou no arquivo, rodar o programa.
            valor = float(saldo) #transformei para float pois saldo estava como str.
            valor_debito = float(valor_debito) #transformei para float pois saldo estava como str.
            valor = valor - valor_debito #aqui eu tirei o valor do saldo menos o valor do debito, e salvei na variável valor.    
            #coloquei Tipo da conta: Comum\n pq foi o jeito que eu salvei no txt, para quando o if for igual ao Comum ( tipo da conta ) ele abrir do jeito que está escrito na linha
            #por isso o uso do readlines[1] nos ifs, para ele ler oq está escrito na linha 1 do txt, que é o "Tipo da conta: Comum\n", e o mesmo para os outros.
            Comum = "Tipo da conta: Comum\n"
            Salario = "Tipo da conta: Salário\n"
            Plus = "Tipo da conta: Plus\n"
        #O readlines [1] serve para ele pegar o que está na 1 linha do programa (tipo de conta), no caso se for Salário
            if Salario in open("Cliente" + cpf +".txt", "r").readlines()[1]:
                #Taxa quando for debitar
                taxacao = 0.95
                #Taxa padrao da conta salário, coloquei como texto, para imprimir no extrato a Tarifa: 5%
                taxa = '5%'
                #aqui eu peguei o valor que será debitado e multipliquei com a taxacao
                dct = valor_debito * taxacao
                #o juros será cobrado da seguinte forma, o valor a ser debitado menos o dct
                juros = valor_debito - dct
                #o valor final é o valor que ficou na conta - o juros.
                final = valor - juros
                #Se o final que é o valor da conta - o valor que está debitando - o valor do juros for menor do que 0, printará erro, pois conta Salário não pode ficar inferior a 0. 
                if final < 0:
                    return print("***Não foi possivel completar essa operação, seu saldo é inferior ao débito! :(***")

        #O readlines [1] serve para ele pegar o que está na 1 linha do programa (tipo de conta), no caso se for Comum
            elif Comum in open("Cliente" + cpf +".txt", "r").readlines()[1]:
                taxacao = 0.97 #Taxa quando for debitar
                #Taxa padrao da conta comum, e irá printar a tarifa que a conta teve
                taxa = '3%'
                #aqui eu peguei o valor que será debitado e multipliquei com a taxacao
                dct = valor_debito * taxacao
                 #o juros será cobrado da seguinte forma, o valor a ser debitado menos o dct
                juros = valor_debito - dct
                #o valor final é o valor que ficou na conta - o juros.
                final = valor - juros
                #Se o final que é o valor da conta - o valor que está debitando - o valor do juros for menor do que -500, printará erro, pois conta Comum não pode ficar inferior a -500.
                if final < -500:
                    return print("***Não foi possivel completar essa operação, seu saldo é inferior ao débito! :(***")
                    
        #O readlines [1] serve para ele pegar o que está na 1 linha do programa (tipo de conta), no caso se for Plus
            elif Plus in open("Cliente" + cpf +".txt", "r").readlines()[1]:
                taxacao = 0.99
                #Taxa padrao da conta tarifa, e irá printar a tarifa que a conta teve
                taxa = '1%'
                #aqui eu peguei o valor que será debitado e multipliquei com a taxacao
                dct = valor_debito * taxacao
                #o juros será cobrado da seguinte forma, o valor a ser debitado menos o dct
                juros = valor_debito - dct
                #o valor final é o valor que ficou na conta - o juros.
                final = valor - juros
                #Se o final que é o valor da conta - o valor que está debitando - o valor do juros for menor do que -5000, printará erro, pois conta Plus não pode ficar inferior a -5000.
                if final < -5000:
                    return print("***Não foi possivel completar essa operação, seu saldo é inferior ao débito! :(***")
            #depois de passar pelos ifs, e ver qual conta está operando, ele gravará a ação feita no Extrato, abrindo o arquivo abaixo:
            novo_txt = open(cpf +".txt", "a")
            data = datetime.now() #aqui serve para colocar e printar a data, da função já do import
            data = data.strftime("%d/%m/%Y %H:%M") #Aqui ele pegará o dia mes ano hora e minuto
            data = str(data) #neste ponto, tranformei data para str e salvei numa variável com o mesmo nome
            #Tarifa mudará conforme o tipo de conta da pessoa., mas enquanto isso, fica como txt Tarifa: 0.00
            novo_txt.write("%s    -    %.2f     Tarifa: 0.00    Saldo:       %.2f  \n" %  (data, valor_debito, final)) #Este .write serve para imprimir os dados igual o do exemplo do professor, mas com as mudanças necessárias usando o %
            novo_txt.close() #Fechei o arquivo
            novo_txt = open("Cliente" + cpf +".txt", 'w') #Aqui eu abri um arquivo do cliente, não do extrato, para salvar os dados depois do débito feito.
            #aqui ele vai pegar os indices que estão na lista que sao os respectivos nomes, tipo_conta, etc.
            #aqui ele vai pegar os indices que estão na lista que sao os respectivos nomes, tipo_conta, etc.
            novo_txt.write(lista[0])
            novo_txt.write(lista[1])
            novo_txt.write("Valor da conta: "+ str(final) + "\n") #Tive que transformar o final para str, pois estava printando erro.
            novo_txt.write(lista[3])
            novo_txt.close() #aqui eu fechei o arquivo
            print() #Print vazio para pular linha
            print("***Valor debitado com sucesso!***") # Printará a mensagem caso tudo ocorrá bem
            print() #Print vazio para pular linha.
        else: # se a senha digitada estiver errada:
            print() #Printará uma linha vazia, apenas para pular a mesma.
            print("***Senha incorreta!***") #printará senha incorreta.
            print() #Printará uma linha vazia, apenas para pular a mesma.

#Função para depositar valores na conta do cliente, com parâmetros para facilitar.
def Deposita(cpf, valor_deposito):
        #abri em modo leitura para poder fazer um for com essa leitura e a criação da lista para colocar tudo que está dentro do 'novo_txt' na lista e posteriormente no for.
        novo_txt = open("Cliente" + cpf +".txt", 'r')
        lista = novo_txt.readlines() #salvei todos os dados desse arquivo na variável lista.
        novo_txt.close()#fechei o arquivo
        #Guardarsenha e Guardarvalor, serve para guardar os valores achados posteriormente no if do "Senha" e no if do "Valor" que ele rastreará no lista[x].
        guardarvalor = ""
        guardarsenha = ""
        for x in range(len(lista)): #ele vai procurar o que está dentro da lista
            #se o 'Valor' estiver na lista, ele vai guardar o valor na lista[x].
            if "Valor" in lista[x]:
                guardarvalor = lista[x]
            #se o 'Senha' estiver na lista, ele vai guardar a senha na lista[x].    
            if "Senha" in lista[x]:
                guardarsenha = lista[x]
        #saldo e saldosenha é para guardar em valores separados e pegar sempre o último elemento        
        saldo = guardarvalor.split(' ')[-1]
        saldosenha = guardarsenha.split(' ')[-1]
        #transformei para float pois saldo estava como str.
        valor = float(saldo)
        #transformei para float pois valor_depósito estava como str, e para não dar erro no print do novo_txt ele precisava estar como float.
        valor_deposito = float(valor_deposito)
        valor = valor + valor_deposito #aqui eu peguei o valor que estava na conta e adicionei o do deopsito
        novo_txt = open("Cliente" + cpf +".txt" , 'w') #abri um arquivo do próprio cliente, não do extrato, em modo w, para poder escrever os dados novos dentro do arquivo.
        #Aqui estou apenas pegando indice 0, 1, 3 para pegar o que está dentro da lista nesses indices e já printar de uma vez, invés de ter q escrever novamente.
        novo_txt.write(lista[0])
        novo_txt.write(lista[1])
        novo_txt.write("Valor da conta: "+ str(valor) + "\n")  #Tive que transformar o valor para str, pois estava printando erro.
        novo_txt.write(lista[3])
        novo_txt.close() #aqui eu fechei o arquivo
        print() #Printará uma linha vazia, apenas para pular a mesma.
        print("***Valor depositado com sucesso!***") #printará a mensagem de valor depositado.
        print() #Printará uma linha vazia, apenas para pular a mesma.
        novo_txt = open(cpf +".txt", "a") #abri o arquivo do cliente do extrato, não do próprio cliente.
        data = datetime.now() # função para printar a data certinha.
        data = data.strftime("%d/%m/%Y %H:%M")#aqui ele estará pegando o dia mes ano hora e minuto que está sendo realizado a ação
        data = str(data) #transformei data em str, numa variável com o mesmo nome.
        #Tarifa mudará conforme o tipo de conta da pessoa., mas enquanto isso, fica como txt Tarifa: 0.00
        novo_txt.write("%s    +    %.2f        Tarifa: 0.00   Saldo:   %.2f  \n" %  (data, valor_deposito,valor)) #Este .write serve para imprimir os dados igual o do exemplo do professor, mas com as mudanças necessárias usando o %
        novo_txt.close() #fechei o arquivo

#Função para consultar o saldo do cliente.
def Saldo(cpf, senha):
    novo_txt = open("Cliente" + cpf +".txt", 'r') #Abri este arquivo dos dados do cliente, não do extrato.
    lista = novo_txt.readlines()#salvei tudo que está dentro deste arquivo numa variável lista
    novo_txt.close()#fechei o arquivo
    #Guardarsenha, serve para guardar os valores achados posteriormente no if do "Senha" que ele rastreará no lista[x].
    guardarsenha = ""
    for x in range(len(lista)): #ele vai procurar o que está dentro da lista
        #se o 'Senha' estiver na lista, ele vai guardar a senha na lista[x].    
        if "Senha" in lista[x]:
            guardarsenha = lista[x]
    #guardarsenha é para guardar em valores separados e pegar sempre o último elemento
    senha_entrar = guardarsenha.split(' ')[-1]
    #função para ver se a senha digitada pelo usuário é igual a senha da conta do cliente, se for vai rodar tudo perfeitamente para poder rodar o Saldo.
    if senha == senha_entrar:
        #se a senha estiver certa, abrir o saldo da conta.
        novo_txt = open("Cliente" + cpf +".txt", 'r') #abri o arquivo do cliente, não do extrato.
        lista = novo_txt.readlines() #nomeei uma variavel qualquer apenas para guardar o readlines dentro dela, para posteriormente chamar no for.
        for x in range(len(lista)): #ele vai procurar o que está dentro da lista
            if "Valor" in lista[x]: #se o valor estiver dentro da lista, efetuará a ação descrita abaixo.
                guardarvalor = lista[x]
                #O interessante é que a cada novo débito, assim que você vier ver o saldo, ele estará atualizado!
                print()  #printará uma linha vazia para poder pula-lá
                print(guardarvalor) #printará o guardarvalor
                print()  #printará uma linha vazia para poder pula-lá
        novo_txt.close() #fechei o arquivo
    else: # se a senha digitada for diferente da senha do cliente:
        print() #Printará uma linha vazia para pdoer pula-lá
        print("***Senha incorreta!***") #printará senha incorreta
        print() #printará uma linha vazia para poder pula-lá          

#Função para consultar histórico completo de tudo que foi feito na conta.
def Extrato(cpf, senha):
    novo_txt = open("Cliente" + cpf +".txt", "r") #abri o arquivo do cliente, não do extrato.
    lista = novo_txt.readlines() #nomeei uma variavel qualquer apenas para guardar o readlines dentro dela, para posteriormente chamar no for.
    novo_txt.close() #fechei o arquivo
    #guardarsenha é para guardar em valores separados e pegar sempre o último elemento
    guardarsenha = ""
    for x in range(len(lista)): #ele vai procurar o que está dentro da lista
        #se o 'Senha' estiver na lista, ele vai guardar a senha na lista[x]. 
        if "Senha" in lista[x]:
            guardarsenha = lista[x]
    #guardarsenha é para guardar em valores separados e pegar sempre o último elemento
    senha_entrar = guardarsenha.split(' ')[-1]
    if senha == senha_entrar:
        #printará o extrato do cliente.
        for x in open(cpf +".txt", "r").readlines(): #aqui ele está pegando tudo que estiver dentro do extrato para printar
            print(x)

#Acesso ao menu de opções com input para direcionar para alguma função. O func é diferente de 0, pq quando for 0, é para parar o programa.
while func != 0:
    print("****Bem-Vindo ao banco QuemPoupaTem!****") #Mensagem de boas vindas
    print() #Print vazio para pular linha
    print("**Menu**") #printará o 'Menu'
    print("1 - Novo Cliente") #se digitar 1, executará a função novo cliente
    print("2 - Apaga Cliente") #se digitar 2, executará a função apaga cliente
    print("3 - Debita") #se digitar 3, executará a função debita
    print("4 - Deposita") #se digitar 4, executará a função deposita
    print("5 - Saldo") #se digitar 5, executará a função saldo
    print("6 - Extrato")#se digitar 6, executará a função extrato
    print("0 - Sai")#se digitar 0, sai do programa.
    print()#Print vazio para pular linha
    func = int(input("Digite a operação desejada: ")) #entrada para saber qual função é a desejada pelo cliente.

    #Se a func for igual a 1, é para cadastrar um novo cliente, não coloquei .split nessa pq de alguma forma o valor_inicial estava dando erro se não fosse float. :(
    if func == 1:
        nome = str(input("Digite seu Nome: ")) # o cliente digitará seu nome
        cpf = str(input("Digite seu CPF: ")) # O cliente digitará seu cpf
        tipo_conta = str(input("Digite o tipo de conta desejado: ('Comum', 'Plus' ou 'Salario')Obs.: Com o maiúsculo primeiro. : ")) #O cliente digitará o tipo de conta desejado
        valor_inicial = float(input("Digite um valor inicial para sua conta: ")) # o cliente digitará um valor inicial
        senha = str(input("Digite sua nova senha: ")) #o cliente digitará uma nova senha
        #Chamando a função novo_cliente já com os parâmetros sendo passados
        novo_cliente(nome, cpf, tipo_conta, valor_inicial, senha) #pegando a função novo cliente e colocando os parâmetros

    #Se a func for igual a 2, é para apagar os dados do cliente.
    if func == 2:
        #Chamando a função Apaga_cliente , não precisou de parâmetros, pois é só apagar, conforme a função vai proceder lá em cima.
        Apaga_Cliente()

    #Se a func for igual a 3, é para debitar da conta do cliente.
    if func == 3:
        cpf, senha, valor_debito = input("Digite seu CPF, sua senha e o valor do débito (sem ponto. Ex: 1000 e não 1.000): ").split(" ") #o cliente digitará seus dados, para poder debitar caso os dados estejam certos.
        #Chamando a função Debita já com os parâmetros sendo passados.
        Debita(cpf, senha, valor_debito) #pegando a função Debita e colocando os parâmetros.

    #Se a func for igual a 4, é para depositar dinheiro na conta do cliente.    
    if func == 4:
        cpf, valor_deposito = input("Digite seu CPF e o valor do deposito (sem ponto. Ex: 1000 e não 1.000): ").split(" ")  #o cliente digitará seus dados, para poder depositar caso os dados estejam certos.
        #Chamando a função Deposita já com os parâmetros sendo passados
        Deposita(cpf, valor_deposito) #pegando a função Deposita e colocando os parâmetros.
    
    #Se a func for igual a 5, é para printar o saldo do cliente atualizado.
    if func == 5:
        cpf, senha = input("Digite seu CPF e sua senha para consultar o saldo: ").split(" ")  #o cliente digitará seus dados, para poder ver seu saldo caso os dados estejam certos.
        #Chamando a função Saldo já com os parâmetros sendo passados
        Saldo(cpf, senha) #pegando a função saldo e colocando os parâmetros.

    #Se a func for igual a 6, é para printar o extrato com todo o histórico que a conta tem.
    if func == 6:
        cpf, senha = input("Digite seu CPF e sua senha para consultar o extrato: ").split(" ")  #o cliente digitará seus dados, para poder ver o extrato caso os dados estejam certos.
        #Chamando a função Extrato já com os parâmetros sendo passados.
        Extrato(cpf, senha) #pegando a função Extrato e colocando os parâmetros.
