import pandas as pd

#Criando um DataFrame inicial

df = pd.DataFrame(columns=['codigo', 'produto', 'quantidade', 'reservado', 'saldo'])

def adicionar_estoque(df,codigo, produto, quantidade, reservado, saldo):
    produtos = pd.DataFrame({                                                                                                                                           
        'codigo': [codigo],
        'produto': [produto],
        'quantidade': [quantidade],
        'reservado': [reservado],
        'saldo': [saldo],
    })
    df = pd.concat([df, pd.DataFrame(produtos)], ignore_index=True)
    return df
df = adicionar_estoque(df, 1, 'produtoA', 100, 0, 100)
df = adicionar_estoque(df, 2, 'produtoB', 50, 0, 50)

def remover_estoque(df):
    while True:
        remover_saldo = input('deseja retirar unidade do estoque: [S]im, [N]ao')
        if remover_saldo.upper() == 'S':
            codigo_produto = int(input('digite o codigo do produto:'))
            try:
                quantidade = float(input('qual quantidade deseja retirar:'))
                #encontrar produto pelo codigo.
                produto = df[df['codigo'] == codigo_produto] 
                
                if produto.empty:
                    print(f'produto com codigo {codigo_produto} nao encontrado')
                else:                                                                                                       
                    if quantidade <= produto['saldo'].values[0]:
                        df.loc[df['codigo'] == codigo_produto, 'saldo'] -= quantidade
                        print(f'foram retirado {quantidade} unidades')
                    else:
                        print(f'quantidade insuficiente em estoque para retirar')
            except ValueError:
                print("Valor invalido.Digite um numero")
        elif remover_saldo.upper() == 'N':
            break
        else:
            print('opcao invalida:Digite S ou N')

def listar_estoque(df):
    while True:
        valores = input("Deseja listar o estoque: [Sim, [N]ao")
        if valores.upper() == 'S':
            print(df.to_string(index=False))
        elif valores.upper() == 'N':
            break
        else:
            print('Digite valores validos')
remover_estoque(df)
listar_estoque(df)
