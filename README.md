import os
import time

def remove_empty_folders(path):
    for root, dirs, files in os.walk(path, topdown=False):
        for dir_name in dirs:
            dir_path = os.path.join(root, dir_name)
            try:
                if not os.listdir(dir_path):  # Verifica se a pasta está vazia
                    print(f"Removendo pasta vazia: {dir_path}")
                    os.rmdir(dir_path)  # Remove a pasta vazia
            except PermissionError:
                print(f"Permissão negada: {dir_path}")
            except Exception as e:
                print(f"Erro ao processar {dir_path}: {e}")

if __name__ == "__main__":
    drive = "C:\\"  # Define o diretório raiz para a varredura
    print(f"Iniciando varredura automática no disco {drive} a cada 2 minutos...")
    print("Pressione Ctrl+C para interromper o processo.\n")
    
    try:
        while True:
            print(f"\n--- Iniciando varredura em {time.strftime('%Y-%m-%d %H:%M:%S')} ---")
            remove_empty_folders(drive)
            print(f"--- Varredura concluída. Próxima verificação em 2 minutos ---")
            time.sleep(120)  # 120 segundos = 2 minutos
            
    except KeyboardInterrupt:
        print("\nVarredura automática interrompida pelo usuário.")
