1. Overview
This Python script creates a GUI-based Google Translator application using Tkinter for UI, Googletrans for translation, and TextBlob for language detection and translation.

2. Required Libraries
tkinter: For creating the graphical user interface (GUI).
googletrans: For translation support.
TextBlob: For automatic language detection and translation.

4. Importing Required Modules
from tkinter import * 
from tkinter import ttk, messagebox
import googletrans
from googletrans import Translator, LANGUAGES
import textblob
from textblob import TextBlob
tkinter: Standard Python library for GUI applications.
ttk: Themed widgets for better styling.
googletrans: Used for translation services.
TextBlob: Used for detecting the language of the input text.


6. Creating the Main Application Window

root = Tk()
root.title("Google Translator")
root.geometry("1080x400")
Tk(): Initializes the main window.
title(): Sets the title of the window.
geometry(): Defines the window size as 1080x400 pixels.


6. Function to Update Language Labels
def label_change():
    c = combo1.get()
    c1 = combo2.get()
    label1.configure(text=c)
    label2.configure(text=c1)
    root.after(1000, label_change)
Updates the labels dynamically based on selected languages in the dropdown menus.
root.after(1000, label_change): Calls the function every 1 second to update the labels.


8. Function to Perform Translation
def translate_now():
    global language

    text_ = text1.get(1.0, END)
    c2 = combo1.get()
    c3 = combo2.get()

    if text_:
        words = textblob.TextBlob(text_)
        lan = words.detect_language()

        for i, j in language.items():
            if j == c3:
                lan_ = i
        
        words = words.translate(from_lang=lan, to=str(lan_))
        text2.delete(1.0, END)
        text2.insert(END, words)  

Steps in Translation:
Gets the input text from the first text box.
Detects the source language using TextBlob.detect_language().
Matches the target language selected in the dropdown (combo2).
Translates the text using TextBlob.translate(from_lang=lan, to=lan_).
Displays the translated text in the second text box.


7. Setting Window Icon
image_icon = PhotoImage(file="ggl.png")
root.iconphoto(False, image_icon)
Sets an icon image for the application.


9. Displaying Arrow Image
arrow_image = PhotoImage(file="arro.png")
image_label = Label(root, image=arrow_image, width=150)
image_label.place(x=460, y=50)
Displays an arrow image between the input and output text areas.


11. Creating Language Dropdown Menus
language = googletrans.LANGUAGES
languageV = list(language.values())
lang1 = language.keys()
Fetches available languages from Googletrans.
Stores them in a list (languageV) for dropdown options.


13. Creating First Language Selection Dropdown
combo1 = ttk.Combobox(root, values=languageV, font="Roboto 14", state="r")
combo1.place(x=110, y=20)
combo1.set("ENGLISH")
Dropdown menu for selecting the source language.
Defaults to "ENGLISH".


15. Creating First Language Label and Input Text Box
label1 = Label(root, text="ENGLISH", font="segoe 30 bold", bg="white", width=18, bd=5, relief=GROOVE)
label1.place(x=10, y=50)

f = Frame(root, bg="Black", bd=5)
f.place(x=10, y=118, width=440, height=210)

text1 = Text(f, font="Robote 20", bg="white", relief=GROOVE, wrap=WORD)
text1.place(x=0, y=0, width=430, height=200)

scrollbar1 = Scrollbar(f)
scrollbar1.pack(side="right", fill="y")

scrollbar1.configure(command=text1.yview)
text1.configure(yscrollcommand=scrollbar1.set)
Label: Displays the selected source language.
Text: Creates a text input box for entering the text to be translated.
Scrollbar: Adds a scrollbar to the text box.


Summary of Features are:
Tkinter GUI for a simple user interface.
Googletrans & TextBlob for language translation.
Dropdown menus to select languages dynamically.
Text areas for input and translated text.
Auto-updating labels for selected languages.
Scrollbar support for better usability.
Translate button to trigger translation.
Uses both Googletrans & TextBlob, making it efficient.


12. Creating Second Language Selection Dropdown
combo2 = ttk.Combobox(root, values=languageV, font="Roboto 14", state="r")
combo2.place(x=730, y=20)
combo2.set("SELECT LANGUAGE")
Dropdown menu for selecting the target language.


14. Creating Second Language Label and Output Text Box

label2 = Label(root, text="ENGLISH", font="segoe 30 bold", bg="white", width=18, bd=5, relief=GROOVE)
label2.place(x=620, y=50)

f1 = Frame(root, bg="Black", bd=5)
f1.place(x=620, y=118, width=440, height=210)

text2 = Text(f1, font="Robote 20", bg="white", relief=GROOVE, wrap=WORD)
text2.place(x=0, y=0, width=430, height=210)

scrollbar2 = Scrollbar(f1)
scrollbar2.pack(side="right", fill="y")

scrollbar2.configure(command=text2.yview)
text2.configure(yscrollcommand=scrollbar2.set)
Label: Displays the selected target language.
Text: Creates a text output box for displaying the translated text.
Scrollbar: Adds a scrollbar to the text box.


14. Adding Translate Button
translate = Button(root, text="Translate", font="Roboto 15 bold italic",
                   activebackground="purple", cursor="hand2", bd=5,
                   bg="red", fg="white", command=translate_now)
translate.place(x=480, y=250)
Creates a "Translate" button.
Calls translate_now() when clicked.


16. Calling Label Change Function
label_change()
Ensures labels update automatically when languages are changed.


18. Configuring Window Background and Running Application
root.configure(bg="white")
root.mainloop()
configure(bg="white"): Sets background color.
mainloop(): Runs the application.
