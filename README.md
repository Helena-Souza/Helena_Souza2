### Organizador de Arquivos por Data de Criação com Python

import os
import shutil
from datetime import datetime

# Defina o caminho da pasta que você quer organizar
caminho_origem = "C:/Users/SeuUsuario/Downloads/Pasta_Bagunçada"

def organizar_arquivos(diretorio):
    # Lista todos os arquivos na pasta
    arquivos = [f for f in os.listdir(diretorio) if os.path.isfile(os.path.join(diretorio, f))]

    for arquivo in arquivos:
        caminho_completo = os.path.join(diretorio, arquivo)
        
        # Obtém a data de modificação do arquivo
        timestamp = os.path.getmtime(caminho_completo)
        data = datetime.fromtimestamp(timestamp)
        
        # Cria o nome da pasta (Ex: 2024-05_Maio)
        nome_pasta = data.strftime("%Y-%m_%B")
        caminho_destino = os.path.join(diretorio, nome_pasta)

        # Se a pasta não existir, cria ela
        if not os.path.exists(caminho_destino):
            os.makedirs(caminho_destino)

        # Move o arquivo para a nova pasta
        shutil.move(caminho_completo, os.path.join(caminho_destino, arquivo))
        print(f"Movido: {arquivo} -> {nome_pasta}")

if __name__ == "__main__":
    organizar_arquivos(caminho_origem)
    print("\n✅ Organização concluída!")
