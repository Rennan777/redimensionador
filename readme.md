# Redimensionador de Imagens

Uma aplicação simples para auxiliar no redimensionamento das imagens a serem enviadas via email.

## Instalação

Use o [pip](https://pip.pypa.io/en/stable/) para instalar as do "requirements.txt".

```bash
pip install -r requirements.txt
```

## Código

```from tkinter import Tk, Label, Button, filedialog, messagebox
from PIL import Image
import os

class RedimensionadorImagens:
    def __init__(self, janela):
        self.janela = janela
        janela.title("Redimensionador de Imagens")

        self.label_entrada = Label(janela, text="Selecione a pasta de entrada:")
        self.label_entrada.pack()

        self.botao_selecionar_entrada = Button(janela, text="Selecionar Pasta", command=self.selecionar_pasta_entrada)
        self.botao_selecionar_entrada.pack()

        self.label_saida = Label(janela, text="Selecione a pasta de saída:")
        self.label_saida.pack()

        self.botao_selecionar_saida = Button(janela, text="Selecionar Pasta", command=self.selecionar_pasta_saida)
        self.botao_selecionar_saida.pack()

        self.botao_redimensionar = Button(janela, text="Redimensionar", command=self.redimensionar_imagens)
        self.botao_redimensionar.pack()

        self.pasta_entrada = ""
        self.pasta_saida = ""

    def selecionar_pasta_entrada(self):
        self.pasta_entrada = filedialog.askdirectory()
        print(f"Pasta de entrada selecionada: {self.pasta_entrada}")

    def selecionar_pasta_saida(self):
        self.pasta_saida = filedialog.askdirectory()
        print(f"Pasta de saída selecionada: {self.pasta_saida}")

    def redimensionar_imagens(self):
        if not self.pasta_entrada or not self.pasta_saida:
            print("Selecione ambas as pastas antes de redimensionar.")
            return

        largura_alvo = 600  # Especifica a largura desejada
        altura_alvo = 800   # Especifica a altura desejada

        for nome_arquivo in os.listdir(self.pasta_entrada):
            caminho_arquivo_entrada = os.path.join(self.pasta_entrada, nome_arquivo)

            if os.path.isfile(caminho_arquivo_entrada) and nome_arquivo.lower().endswith(('.png', '.jpg', '.jpeg', '.gif')):
                imagem = Image.open(caminho_arquivo_entrada)
                nova_imagem = imagem.resize((largura_alvo, altura_alvo), resample=Image.LANCZOS)

                caminho_arquivo_saida = os.path.join(self.pasta_saida, nome_arquivo)
                nova_imagem.save(caminho_arquivo_saida)

        messagebox.showinfo('Sucesso','As imagens foram redimensionadas com sucesso.')

if __name__ == "__main__":
    root = Tk()
    root.geometry("400x200")
    app = RedimensionadorImagens(root)
    root.mainloop()
```

## Contribuições

Sinta-se livre para adequar ao seu caso de uso.