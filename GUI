from tkinter import *
from PIL import Image, ImageTk
import os

def you():
    os.system('python Assistance.py')


root =Tk()
root.geometry("755x744")
image = Image.open("google.jpeg")
photo = ImageTk.PhotoImage(image)
fu_label = Label(image=photo)
fu_label.pack()

root.geometry("655x333")

frame = Frame(root,bg="grey",relief=SUNKEN)
frame.pack(side=LEFT,anchor="nw")
b1=Button(frame,fg="blue", text="Click to activate assistant",command=you)
b1.pack(side=BOTTOM,padx=253)
root.mainloop()
