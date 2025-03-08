import tkinter as tk
from tkinter import filedialog
from tkinter import messagebox
from fpdf import FPDF

# Function to open a file using file dialog
def open_file():
    file_path = filedialog.askopenfilename(title="Open a text file", filetypes=[("Text Files", "*.txt")])
    
    if file_path:  # If a file is selected
        try:
            with open(file_path, 'r') as file:
                file_contents = file.read()
                text_area.delete(1.0, tk.END)  # Clear previous contents
                text_area.insert(tk.END, file_contents)  # Display the file contents
                root.title(f"Viewing: {file_path}")  # Update the window title
                global current_file_path
                current_file_path = file_path  # Store the file path for later use
        except Exception as e:
            messagebox.showerror("Error", f"Could not open the file: {e}")
    else:
        messagebox.showinfo("No File", "No file was selected.")

# Function to convert txt to pdf
def convert_to_pdf():
    if 'current_file_path' not in globals():
        messagebox.showerror("No File", "Please open a text file first.")
        return
    
    try:
        # Get the content of the text area (or you can read the file directly)
        text_content = text_area.get(1.0, tk.END)
        
        # Create PDF object
        pdf = FPDF()
        pdf.add_page()
        
        # Set font for the PDF
        pdf.set_font("Arial", 'B', 16)
        
        # Add Title
        pdf.cell(200, 10, txt="Text File to PDF", ln=True, align='C')
        pdf.ln(10)  # Line break

        # Set font for the content
        pdf.set_font("Arial", size=12)
        
        # Add the text content to the PDF
        pdf.multi_cell(0, 10, text_content)
        
        # Add Page number
        pdf.ln(10)
        pdf.set_font("Arial", 'I', 8)
        pdf.cell(0, 10, f"Page {pdf.page_no()}", 0, 0, 'C')

        # Ask where to save the PDF
        output_pdf_path = filedialog.asksaveasfilename(defaultextension=".pdf", filetypes=[("PDF Files", "*.pdf")])
        
        if output_pdf_path:  # If the user chooses a location to save
            pdf.output(output_pdf_path)
            messagebox.showinfo("Success", f"PDF saved as {output_pdf_path}")
        else:
            messagebox.showinfo("No File", "No location selected for saving the PDF.")
    except Exception as e:
        messagebox.showerror("Error", f"Could not convert to PDF: {e}")

# Create the main window
root = tk.Tk()
root.title("TXT to PDF Converter")
root.geometry("600x400")

# Create a button to open a file
open_button = tk.Button(root, text="Open TXT File", command=open_file)
open_button.pack(pady=20)

# Create a button to convert text to PDF
convert_button = tk.Button(root, text="Convert to PDF", command=convert_to_pdf)
convert_button.pack(pady=10)

# Create a Text widget to display the file contents
text_area = tk.Text(root, wrap=tk.WORD, width=70, height=15)
text_area.pack(padx=20, pady=10)

# Start the GUI event loop
root.mainloop()
