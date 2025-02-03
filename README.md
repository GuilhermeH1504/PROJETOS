import json

def carregar_clientes(caminho_arquivo):
    try:
        with open(caminho_arquivo, 'r', encoding='utf-8') as arquivo:
            return json.load(arquivo)
    except FileNotFoundError:
        print('arquivo nao encontrado')
        return [] 
    except json.JSONDecodeError as e:
        print(f'Erro ao ler o arquivo JSON: {e}')
        return []
def salvar_clientes(caminho_arquivo, clientes):
    with open(caminho_arquivo, 'w', encoding='utf-8') as arquivo:
        json.dump(clientes, arquivo, indent=2)

# Filtrar clientes        
def clientes_situacao(situacao_ativo, situacao_inativo, clientes):
    while True:
        situacoes = input('Deseja filtrar os clientes por situacao: [A]tivos, [I]nativos, [V]oltar:')
        if situacoes.upper() == 'A':
            for item in clientes:
                if item['situacao'] == situacao_ativo:
                    print(json.dumps(item, indent=2))
        elif situacoes.upper() == 'I':
                    for item in clientes:
                        if item['situacao'].strip().lower() == situacao_inativo.lower():
                            print(json.dumps(item, indent=2))
        elif situacoes.upper() == 'V':
            break
        else:
            print('Digite valores validos: [A]tivos, [I]nativos:')
# Listar clientes 
def listar_clientes(clientes):
    while True:
        valores = input('Deseja listar os clientes: [S]im, [N]ao')
        if valores.upper() == 'S':
            print(json.dumps(clientes, indent=2))
        elif valores.upper() == 'N':
            break
        else:
            print('Digite valores validos: [S]im ou [N]ao')
# Menu de iteracao 
def main():
    while True:
        print('Selecione uma opcao:')
        print('F - Filtrar clientes por situacao')
        print('L - Listar clientes')
        print('S - sair')
        opcoes = input('Escolha uma opcao:')
        if opcoes.upper() == 'F':
            clientes_situacao('ativo', 'inativo', carregar_clientes('clientes.json'))
        elif opcoes.upper() == 'L':
            listar_clientes(carregar_clientes('clientes.json'))
        elif opcoes.upper() == 'S':
            break
        else:
            print('Digite alguma lera das opcoes:')
if __name__ == "__main__":
    main()
