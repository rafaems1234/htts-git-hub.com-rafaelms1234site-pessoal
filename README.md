import datetime

# Variáveis globais
saldo = 0.0
extrato = []
limite_saque = 500.0
qtd_max_saques = 3
saques_realizados = 0
tarifa_saque = 2.50
data_hoje = datetime.date.today()

def depositar():
    global saldo
    valor = float(input("Informe o valor para depósito: R$ "))
    if valor > 0:
        saldo += valor
        extrato.append(f"{datetime.datetime.now()} - Depósito: +R$ {valor:.2f}")
        print(f"Depósito de R$ {valor:.2f} realizado com sucesso!")
    else:
        print("Valor inválido para depósito.")

def sacar():
    global saldo, saques_realizados, data_hoje

    if datetime.date.today() != data_hoje:
        saques_realizados = 0
        data_hoje = datetime.date.today()

    if saques_realizados >= qtd_max_saques:
        print("Limite diário de saques atingido.")
        return

    valor = float(input("Informe o valor para saque: R$ "))

    if valor <= 0:
        print("Valor inválido.")
    elif valor > limite_saque:
        print(f"Valor acima do limite por saque (R$ {limite_saque:.2f}).")
    elif valor + tarifa_saque > saldo:
        print("Saldo insuficiente para saque com tarifa.")
    else:
        saldo -= (valor + tarifa_saque)
        saques_realizados += 1
        extrato.append(f"{datetime.datetime.now()} - Saque: -R$ {valor:.2f} (Tarifa: R$ {tarifa_saque:.2f})")
        print(f"Saque de R$ {valor:.2f} realizado com sucesso (Tarifa: R$ {tarifa_saque:.2f}).")

def ver_extrato():
    print("\n===== EXTRATO =====")
    if not extrato:
        print("Nenhuma movimentação.")
    else:
        for transacao in extrato:
            print(transacao)
    print(f"\nSaldo atual: R$ {saldo:.2f}")
    print("===================\n")

def menu():
    while True:
        print("=== BANCO PYTHON ===")
        print("1 - Depositar")
        print("2 - Sacar")
        print("3 - Ver Extrato")
        print("4 - Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == '1':
            depositar()
        elif opcao == '2':
            sacar()
        elif opcao == '3':
            ver_extrato()
        elif opcao == '4':
            print("Obrigado por utilizar o Banco Python!")
            break
        else:
            print("Opção inválida!")

# Iniciar o sistema
menu()
