# Proyecto-III

## Presentado por:
### Bryan Josue Alvarez Lopez, Julio Alexander Alvarado Morales y Jonathan Joel Istupe Martinez
###### Bryan Alvarez: 7690-23-16816
###### Julio Alvarado: 7690-23-13706
###### Jonathan Istupe: 7690-23-15804

## Algoritmo
Utilizando el lenguaje de programación Python,  se realizo una aplicación (con interfaz gráfica) que pueda leer un archivo de texto (.txt, .cpp, .cs, .py,) y permite guardar los cambios y la opcion de guardar como,
utilizamos también la libreria de tkinter el cual posee
##### Requisito de aceptacion
###### Abrir
###### Guardar
###### Guardar como
###### (Permite leer y guardar archivos en mas extensiones que solo en txt)

### El video de nuestro tema es:
## https://youtu.be/6Ic70MG71pE

## Python 
```python
import tkinter as tk
import webbrowser
from tkinter import filedialog, messagebox, ttk, simpledialog, colorchooser, scrolledtext

class TextEditorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Text Editor")

        self.text_area = scrolledtext.ScrolledText(self.root, wrap="word", undo=True, bg="black", fg="white")
        self.text_area.pack(expand="yes", fill="both")

        self.root.configure(bg="black")

        self.menu_bar = tk.Menu(self.root, bg="black", fg="white", activebackground="white", activeforeground="black")
        self.root.config(menu=self.menu_bar)

        self.file_menu = tk.Menu(self.menu_bar, tearoff=0)
        self.menu_bar.add_cascade(label="Archivo", menu=self.file_menu)
        self.file_menu.add_command(label="Abrir", command=self.open_file)
        self.file_menu.add_command(label="Guardar", command=self.save_file)
        self.file_menu.add_command(label="Guardar como...", command=self.save_file_as)
        self.file_menu.add_separator()
        self.file_menu.add_command(label="Salir", command=self.root.destroy)

        self.edit_menu = tk.Menu(self.menu_bar, tearoff=0)
        self.menu_bar.add_cascade(label="Editar", menu=self.edit_menu)
        self.edit_menu.add_command(label="Deshacer", command=self.undo)
        self.edit_menu.add_command(label="Rehacer", command=self.redo)

        self.format_menu = tk.Menu(self.menu_bar, tearoff=0)
        self.menu_bar.add_cascade(label="Formato", menu=self.format_menu)
        self.format_menu.add_command(label="Cambiar tamaño de letra", command=self.change_font_size)
        self.format_menu.add_command(label="Cambiar color de texto", command=self.change_text_color)

        self.help_menu = tk.Menu(self.menu_bar, tearoff=0)
        self.menu_bar.add_cascade(label="Ayuda", menu=self.help_menu)
        self.help_menu.add_command(label="Información", command=self.show_info)
        self.help_menu.add_command(label="Manual de usuario", command=self.open_manual)
        self.help_menu.add_command(label="Integrantes", command=self.show_integrantes)

        style = ttk.Style()
        style.configure("TButton", padding=(5, 5, 5, 5), font=('Helvetica', 10))

        self.button_font_size = ttk.Button(self.root, text="Tamaño de letra", command=self.change_font_size)
        self.button_font_size.pack(side=tk.LEFT, padx=5)

        self.button_text_color = ttk.Button(self.root, text="Color de texto", command=self.change_text_color)
        self.button_text_color.pack(side=tk.LEFT, padx=5)

        self.file_path = None

    def open_file(self):
        file_path = filedialog.askopenfilename(filetypes=[("Archivos de texto", "*.txt"), ("Todos los archivos", "*.*")])
        if file_path:
            with open(file_path, "r") as file:
                content = file.read()
                self.text_area.delete("1.0", tk.END)
                self.text_area.insert(tk.END, content)
            self.file_path = file_path

    def save_file(self):
        if self.file_path:
            content = self.text_area.get("1.0", tk.END)
            with open(self.file_path, "w") as file:
                file.write(content)
        else:
            self.save_file_as()

    def save_file_as(self):
        file_path = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Archivos de texto", "*.txt"), ("Todos los archivos", "*.*")])
        if file_path:
            self.file_path = file_path
            self.save_file()

    def undo(self):
        self.text_area.edit_undo()

    def redo(self):
        self.text_area.edit_redo()

    def change_font_size(self):
        size_input = simpledialog.askinteger("Cambiar tamaño de letra", "Ingrese el nuevo tamaño de letra:", parent=self.root)

        if size_input:
            current_font = self.text_area.cget("font")
            new_font = (current_font[0], size_input)
            self.text_area.configure(font=new_font)

    def change_text_color(self):
        color = colorchooser.askcolor()[1]
        if color:
            self.text_area.tag_configure("colored", foreground=color)
            current_index = self.text_area.index(tk.SEL_FIRST)
            if current_index:
                self.text_area.tag_add("colored", current_index, tk.SEL_LAST)
            else:
                self.text_area.tag_add("colored", "1.0", tk.END)

    def show_info(self):
        app_info = "Informacion\n\nEsta aplicación es un editor de texto con una interfaz gráfica utilizando el lenguaje PYTHON y la librería TKinter.\n\nLicencia: MIT License\nVersión: 1.0"
        messagebox.showinfo("Información", app_info)

    def open_manual(self):
        repo_url = "https://github.com/Jonathanjips/Proyecto-III#readme"
        webbrowser.open_new(repo_url)

    def show_integrantes(self):
        app_info = "Estudiantes\n\n Julio Alexander Alvarado Morales\n         7690-23-13706\n\nJonathan Joel Istupe Martinez\n         7690-23-15804\n\nBryan Josué Alvarez López\n         7690-23-16816"
        messagebox.showinfo("Estudiantes", app_info)
        pass

if __name__ == "__main__":
    root = tk.Tk()
    app = TextEditorApp(root)
    root.mainloop()

```

## Gracias por su atencion
## Saludos
