def cadastrar_produto():
    print("\n--- Cadastro de Produto ---")

    nome = input("Nome do produto: ").strip().upper()

    while nome = "":
        print("O nome não pode ficar vazio.")
        nome = input("Nome do produto: ").strip().upper()

    while True:
        try:
            quantidade = int(input("Quantidade: "))

            if quantidade < 0:
                print("A quantidade não pode ser negativa.")
            else:
                break
        except ValueError:
            print("Digite uma quantidade válida.")

    while True:
        try:
            preco = float(input("Preço: R$ ").replace(",", "."))

            if preco < 0:
                print("O preço não pode ser negativo.")
            else:
                break
        except ValueError:
            print("Digite um preço válido.")

    produto = {
        "nome": nome,
        "quantidade": quantidade,
        "preco": preco
    }

    return produto


def calcular_valor_estoque(produto):
    valor = produto["quantidade"] * produto["preco"]
    return valor


def buscar_produto(produtos, nome):
    nome = nome.strip().upper()

    for produto in produtos:
        if produto["nome"] == nome:
            return produto

    return None


def atualizar_estoque(produto, quantidade, operacao):
    if operacao == "entrada":
        produto["quantidade" += quantidade
        return True

    if operacao == "saida":
        if quantidade <= produto["quantidade"]:
            produto["quantidade"] -= quantidade
            return True

    return False


def aplicar_desconto(produto, percentual):
    desconto = produto["preco"] * percentual / 100
    novo_preco = produto["preco"] - desconto

    return novo_preco


def mostrar_estoque(produtos):
    print("\n========== ESTOQUE ==========")

    if len(produtos) == 0:
        print("Nenhum produto cadastrado.")
        return 0

    total = 0

    fr produto in produtos:
        valor = calcular_valor_estoque(produto)
        total += valor

        print(f"\nProduto: {produto['nome']}")
        print(f"Quantidade: {produto['quantidade']}")
        print(f"Preço: R$ {produto['preco']:.2f}")
        print(f"Valor em estoque: R$ {valor:.2f}")

        if produto["quantidade"] == 0:
            print("Status: Estoque esgotado")
        elif produto["quantidade"] <= 5:
            print("Status: Estoque baixo")
        else:
            print("Status: Estoque normal")

    print(f"\nValor total do estoque: R$ {total:.2f}")

    return otal


def menu():
    print("\n==============================")
    print("      GESTÃO DE ESTOQUE")
    print("==============================")
    print("1 - Cadastrar produto")
    print("2 - Mostrar estoque")
    print("3 - Buscar produto")
    print("4 - Entrada de produtos")
    print("5 - Saída de produtos")
    print("6 - Aplicar desconto")
    print("7 - Sair")
    print("==============================")

    return input("Escolha uma opção: ").strip()


 main():
    produtos = []

    while True:
        opcao = menu()

        if opcao == "1":
            produto = cadastrar_produto()
            produtos.append(produto)
            print("Produto cadastrado com sucesso.")

        elif opcao == "2":
            mostrar_estoque(produtos)

        elif opcao == "3":
            nome = input("Digite o nome do produto: ")
            produto = buscar_produto(produtos, nome)

            if produto:
                print("\nProduto encontrado.")
                print(f"Nome: {produto['nome']}")
                print(f"Quantidade: {produto['quantidade']}")
                print(f"Preço: R$ {produto['preco']:.2f}")
            else:
                print("Produto não encontrado.")

        elif opcao == "4":
            nome = input("Digite o nome do produto: ")
            produto = buscar_produto(produtos, nome)

            if produto is None:
                print("Produto não encontrado.")
            else:
                try:
                    quantidade = int(input("Quantidade de entrada: "))

                    if quantidade <= 0:
                        print("Digite uma quantidade maior que zero.")
                    else:
                        atualizar_estoque(
                            produto,
                            quantidade,
                            "entrada"
                        )
                        print("Entrada registrada com sucesso.")

                except ValueError:
                    print("Digite uma quantidade válida.")

        elif opcao == "5":
            nome = input("Digite o nome do produto: ")
            produto = buscar_produto(produtos, nome)

            if produto is None:
                print("Produto não encontrado.")
            else:
                try:
                    quantidade = int(input("Quantidade de saída: "))

                    if quantidade <= 0:
                        print("Digite uma quantidade maior que zero.")
                    elif quantidade > produto["quantidade"]:
                        print("Quantidade maior que o estoque.")
                    else:
                        atualizar_estoque(
                            produto,
                            quantidade,
                            "saida"
                        )
                        print("Saída registrada com sucesso.")

                except ValueError:
                    print("Digite uma quantidade válida.")

        elif opcao == "6":
            nome = input("Digite o nome do produto: ")
            produto = buscar_produto(produtos, nome)

            if produto is None:
                print("Produto não encontrado.")
            else:
                try:
                    percentual = float(
                        input("Digite o desconto (%): ").replace(",", ".")
                    )

                    if percentual < 0 or percentual > 100:
                        print("Digite um valor entre 0 e 100.")
                    else:
                        novo_preco = aplicar_desconto(
                            produto,
                            percentual
                        )

                        print(
                            f"Preço original: "
                            f"R$ {produto['preco']:.2f}"
                        )

                        print(
                            f"Preço com desconto: "
                            f"R$ {novo_preco:.2f}"
                        )

                except ValueError:
                    print("Digite um percentual válido.")

        elf opcao == "7":
            print("Programa encerrado.")
            break

        else:
            print("Opção inválida.")


if __name__ == "__min__":
    main()
