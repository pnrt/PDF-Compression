# **PDF Compression with Ghostscript 🗜️📄**  
[![Ghostscript](https://img.shields.io/badge/Ghostscript-v10.0-blue?logo=ghost)](https://ghostscript.com/releases/)  
[![Python](https://img.shields.io/badge/Python-3.7+-yellow?logo=python)](https://www.python.org/)  
[![License](https://img.shields.io/github/license/pnrt/PDF-compression)](LICENSE)  

A **lightweight and efficient** way to **compress PDFs** using **Ghostscript (`gs`)** while maintaining good image quality.  

---

## **🔧 Installation**  

### **1️⃣ Install Ghostscript**  
#### **📌 macOS (Homebrew)**
```sh
brew install ghostscript
```
#### **📌 Windows**  
1. Download **Ghostscript** from [official site](https://ghostscript.com/releases/).  
2. Install and **add it to your system PATH**.  

#### **📌 Linux (Debian/Ubuntu)**
```sh
sudo apt install ghostscript
```

---

## **🚀 Usage**  

### **🔹 Command Line**
Run the following command to compress a PDF:  
```sh
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dBATCH -sOutputFile=output.pdf input.pdf
```

**🔹 Compression Levels**  
| **Option**   | **Best For** | **Compression Strength** |
|-------------|-------------|--------------------------|
| `/screen`   | Smallest size (low-quality images) | 🔥🔥🔥🔥 |
| `/ebook`    | Good balance for reading | 🔥🔥🔥 |
| `/printer`  | Higher quality for printing | 🔥🔥 |
| `/prepress` | Best for publishing (large files) | 🔥 |

📌 **Example Usage:**
```sh
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook -dNOPAUSE -dBATCH -sOutputFile=compressed.pdf original.pdf
```

---

## **📝 Python Script**  

If you want to automate compression using **Python**, you can use this script:

```python
import subprocess
import os
import tkinter as tk
from tkinter import filedialog, messagebox, ttk

def compress_pdf(input_pdf, output_pdf, quality="screen"):
    """Compress PDF using Ghostscript without losing much quality."""
    gs_command = [
        "gs", "-sDEVICE=pdfwrite",
        "-dCompatibilityLevel=1.4",
        f"-dPDFSETTINGS=/{quality}",
        "-dNOPAUSE", "-dBATCH",
        f"-sOutputFile={output_pdf}",
        input_pdf
    ]

    try:
        subprocess.run(gs_command, check=True)
        original_size = os.path.getsize(input_pdf) / 1024
        compressed_size = os.path.getsize(output_pdf) / 1024
        reduction = 100 - ((compressed_size / original_size) * 100)

        messagebox.showinfo("Success", f"Compressed PDF saved at:\n{output_pdf}\n"
                                       f"Original: {original_size:.2f} KB\n"
                                       f"Compressed: {compressed_size:.2f} KB\n"
                                       f"Size Reduced: {reduction:.2f}%")

    except subprocess.CalledProcessError as e:
        messagebox.showerror("Error", f"Compression failed: {e}")

def browse_pdf():
    """Select a PDF file."""
    file_path = filedialog.askopenfilename(filetypes=[("PDF Files", "*.pdf")])
    if file_path:
        input_entry.delete(0, tk.END)
        input_entry.insert(0, file_path)

def save_pdf():
    """Select save location for the compressed PDF."""
    output_path = filedialog.asksaveasfilename(defaultextension=".pdf",
                                               filetypes=[("PDF Files", "*.pdf")])
    if output_path:
        output_entry.delete(0, tk.END)
        output_entry.insert(0, output_path)

def start_compression():
    """Start the compression process."""
    input_pdf = input_entry.get()
    output_pdf = output_entry.get()
    quality = quality_var.get()

    if not input_pdf or not output_pdf:
        messagebox.showwarning("Warning", "Please select input and output files.")
        return

    compress_pdf(input_pdf, output_pdf, quality)

# UI
root = tk.Tk()
root.title("PDF Compressor")
root.geometry("400x300")

ttk.Label(root, text="Select PDF File:").pack(pady=2)
input_entry = ttk.Entry(root, width=40)
input_entry.pack(pady=2)
ttk.Button(root, text="Browse", command=browse_pdf).pack(pady=2)

ttk.Label(root, text="Save Compressed PDF As:").pack(pady=2)
output_entry = ttk.Entry(root, width=40)
output_entry.pack(pady=2)
ttk.Button(root, text="Save As", command=save_pdf).pack(pady=2)

ttk.Label(root, text="Compression Quality:").pack(pady=2)
quality_var = tk.StringVar(value="screen")
quality_options = ["screen", "ebook", "printer", "prepress"]
quality_menu = ttk.Combobox(root, textvariable=quality_var, values=quality_options, state="readonly")
quality_menu.pack(pady=2)

ttk.Button(root, text="Compress PDF", command=start_compression).pack(pady=10)

root.mainloop()

```

---

## **📸 Screenshots**
#### ✅ **Before Compression**  
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/PDF_icon.svg/800px-PDF_icon.svg.png" width="150">

#### 🔻 **After Compression**  
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Adobe_Acrobat_DC_logo_2020.svg/1024px-Adobe_Acrobat_DC_logo_2020.svg.png" width="150">

---

## **💡 Why Use Ghostscript?**  
✔ **Free & Open Source**  
✔ **High Compression Efficiency**  
✔ **Retains PDF Structure**  
✔ **Works on Windows, macOS, & Linux**  

---

## **📜 License**  
This project is licensed under the **MIT License**. Feel free to use and modify it!

---

## **⭐ Star this repo if you find it useful!**  
[![GitHub Repo stars](https://img.shields.io/github/stars/pnrt/PDF-compression?style=social)](https://github.com/pnrt/PDF-compression)  

---
