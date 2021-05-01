# Morse_GUI
from morse3 import Morse as m
import tkinter as tk
from gpiozero import LED
import RPi.GPIO
import time

RPi.GPIO.setmode(RPi.GPIO.BCM)

led = LED(14)

m("a a23").stringToMorse()

def morseButton():
    word = (text.get()[:12])
    word = m(word).stringToMorse()
    for char in word:
        if char=='-':
            led.on()
            time.sleep(1.5)
            led.off()
            time.sleep(0.5)
        elif char=='.':
            led.on()
            time.sleep(0.5)
            led.off()
            time.sleep(0.5)
        elif char == ' ':
            led.off()
            time.sleep(1.5)
        else:
            break
def exit():
    RPi.GPIO.cleanup()
    window.destroy()
    
window=tk.Tk()
window.minsize(200,200)
window.title("Text to Morse")

label=tk.Label(window,text='Enter word below').grid(column=0,row=0)
text=tk.StringVar()
box=tk.Entry(window,width=12,textvariable=text).grid(column=0,row=1)

runCode=tk.Button(window,text='Run',command=morseButton).grid(column=0,row=2)

ExitButton=tk.Button(window, text = "Exit",command = exit).grid(column=0,row=3)
