# Camera-using-Python
Code for a capturing video and image using python
#EASY CAMERA WITH PYTHON
from easygui import *
import numpy as np
import matplotlib.pyplot as plt #IMPORTING LIBRARIES
import tkinter as tk
from tkinter import simpledialog
import time
import cv2

text="Select any one item"
title="Camera 369"
choices=["Photo","Video"]
output= choicebox(text,title,choices)
title="Camera 369"
message = "You selected: "+str(output)
msg= msgbox(message,title)
time.sleep(3)
if output=="Video":
    mssg="Recording starts in 3 seconds"
    title="Camera 369 "
    mesag=msgbox(mssg,title)
    time.sleep(3)
    
   
    cap=cv2.VideoCapture(1)
    frame_width= int(cap.get(3))
    frame_height= int(cap.get(4))
    vid_cod=cv2.VideoWriter_fourcc(*'XVID')
    USR_INP=simpledialog.askstring(title="Save Video",prompt="File name")
    video_output=cv2.VideoWriter(USR_INP,vid_cod,10,(frame_width,frame_height))
    
    while (True):
        ret,Frame=cap.read()
        if ret==True:
            video_output.write(Frame)
            cv2.imshow('frame',Frame)
            if cv2.waitKey(1) & 0xFF==ord('x'):
                break
    cap.release()
    video_output.release()

   
    ROOT=tk.Tk()
    ROOT.withdraw()
    
                         #IMAGE INTO .jpg FORMAT
                    #SAVED IMAGE
    cv2.destroyAllWindows()




elif output=="Photo":
    a=cv2.VideoCapture(1)               #CAMERA ON(1)
    while True:
        rval,frame=a.read()                 #TO READ THE VIDEO CAPTURED
        cv2.imshow('Captured_Image_Window',frame) #SHOWS IT IN A WINDOW TITLED 'Captured_Image_Window'
        if cv2.waitKey(10) & 0xFF==ord('q'): #WAITKEY IS TO KEEP THE WINDOW FOR 10millisecond and q IS TO CLOSE THE WINDOW
                                                                #AT THE END OF MILLISECOND OR WHEN YOU PRESS q THE IAMGE WILL BE CAPTURED
            break
                                                     #TO SAVE CAPTURED IMAGE
        b,g,r=cv2.split(frame)                  #TO SPLIT CAPTURED IMAGE TO RGB BY SPLITTING IT
        frame_rgb=cv2.merge((r,g,b))        #TO JOIN THE R,G,B IMAGE
        plt.imshow(frame_rgb)                   #FRAME TO SHOW Captured Image
        plt.title('Captured_Image')         #WINDOW TITLE 'Captured_Image'
        plt.show

                                                            #TO CREATE SAVE DIALOG BOX
    ROOT=tk.Tk()
    ROOT.withdraw()
    USER_INP=simpledialog.askstring(title="Save Image",prompt="File name")
    UNP= USER_INP + '.jpg'                     #IMAGE INTO .jpg FORMAT
    cv2.imwrite(UNP,frame)                  #SAVED IMAGE
    cv2.destroyAllWindows()

    
    
    








