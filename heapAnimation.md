# Python_HeapAnimation
#This program shows how a heap is represented as a binary tree
#This program was written in Visual Studio using python 2.7
    import Tkinter
    import tkMessageBox
    items = []

    def bubbleUp(num):
        if num == 0 or (items[num] <= items[parent(num)]):
            return #Do Nothing, No Voilation
        else:
            while(items[num] > items[parent(num)]):
                #Swap Items
                items[num],items[parent(num)] = items[parent(num)],items[num]
                bubbleUp(parent(num))

    def bubbleDown(num):
        length = len(items)
        lChild = leftChild(num)
        rChild = rightChild(num)

        if lChild >= length:#Check if only one element
           return 

        minIndex = num

        if items[num] < items[lChild]:
            minIndex = lChild

        if rChild < length and (items[minIndex] < items[rChild]):
            minIndex = rChild

        if minIndex != num:
            items[minIndex],items[num] = items[num],items[minIndex]
            bubbleDown(minIndex)

    #Index of left child
    def leftChild(num):
        lChild = (2 * num)+1
        return lChild

    #index of right child
    def rightChild(num):
        rChild = (2 * (num +1))
        return rChild

    #Retrieve index of parent
    def parent(num):
        if num%2 == 0: #Even Number
            parentIndex  = (num/2)-1
            return parentIndex
        else: #Odd Number
            parentIndex = (num -1)/2
            return parentIndex

    class MyGUI:
        def __init__(self):
            #Create the main window widget
            self.main_window = Tkinter.Tk()
            self.main_window.wm_title("Heap Animation")

            #Create two frames
            self.top_frame = Tkinter.Frame(self.main_window, height = 500, width = 500)
            self.bottom_frame = Tkinter.Frame(self.main_window)

            #Add a Label
            self.label = Tkinter.Label(self.bottom_frame, text = "Enter a key")

            #Configure textbox
            self.userInput = Tkinter.Entry(self.bottom_frame)

            #Configure 'insert' button
            self.insertButton = Tkinter.Button(self.bottom_frame, text = "Insert",command = self.getData)

            #configure 'delete' button
            self.deleteButton = Tkinter.Button(self.bottom_frame, text = "Delete", command = self.removeData)

            #Create Animations
            #Add a canvas to the top frame
            self.canvasMain = Tkinter.Canvas(self.top_frame, width = 450, height = 350)

            #Call the widgets pack methods(Add items to GUI)
            self.top_frame.pack()
            self.bottom_frame.pack()

            self.label.pack(side = 'left')
            self.userInput.pack(side = 'left')
            self.deleteButton.pack(side = 'right')
            self.insertButton.pack(side = 'right')

            self.canvasMain.pack()

            self.id0 = self.canvasMain.create_text(220,45, text = " ")
            self.id1 = self.canvasMain.create_text(140,120, text = " ")
            self.id2 = self.canvasMain.create_text(290,120, text = " ")
            self.id3 = self.canvasMain.create_text(90,200, text = " ")
            self.id4 = self.canvasMain.create_text(170,200, text = " ")
            self.id5 = self.canvasMain.create_text(250,200, text = " ")
            self.id6 = self.canvasMain.create_text(330,200, text = " ")

            self.circ0 = self.canvasMain.create_oval(0, 0, 0, 0 )
            self.circ1 = self.canvasMain.create_oval(0, 0, 0, 0 )
            self.circ2 = self.canvasMain.create_oval(0, 0, 0, 0 )
            self.circ3 = self.canvasMain.create_oval(0, 0, 0, 0 )
            self.circ4 = self.canvasMain.create_oval(0, 0, 0, 0 )
            self.circ5 = self.canvasMain.create_oval(0, 0, 0, 0 )
            self.circ6 = self.canvasMain.create_oval(0, 0, 0, 0 )

            self.line1 = self.canvasMain.create_line(0,0,0,0)
            self.line2 = self.canvasMain.create_line(0,0,0,0)
            self.line3 = self.canvasMain.create_line(0,0,0,0)
            self.line4 = self.canvasMain.create_line(0,0,0,0)
            self.line5 = self.canvasMain.create_line(0,0,0,0)
            self.line6 = self.canvasMain.create_line(0,0,0,0)

            #Enter the tkinter main loop
            Tkinter.mainloop()

        #Circle for Index 0
        def circle0(self):
            xval = 200
            yval = 25
            self.canvasMain.coords(self.circ0, xval,yval, xval+40, yval+40)  
            self.canvasMain.itemconfig(self.id0,text = str(items[0]))
            self.canvasMain.coords(self.id0, 220,45)

        #Circle for index 1
        def circle1(self):
            xval = 120
            yval = 100
            self.canvasMain.coords(self.circ1, xval,yval, xval+40, yval+40)
            self.canvasMain.coords(self.line1, 200,55,160,110)
            self.canvasMain.itemconfig(self.id1,text = str(items[1]))
            self.canvasMain.coords(self.id1, 140,120)


        def circle2(self):
            xval = 270
            yval = 100
            self.canvasMain.coords(self.circ2, xval,yval, xval+40, yval+40)
            self.canvasMain.coords(self.line2, 240,55,275,105)
            self.canvasMain.itemconfig(self.id2,text = str(items[2]))
            self.canvasMain.coords(self.id2, 290,120)

        def circle3(self):
            xval = 70
            yval = 180
            self.canvasMain.coords(self.circ3, xval,yval, xval+40, yval+40)
            self.canvasMain.coords(self.line3, 100,180,130,135)
            self.canvasMain.itemconfig(self.id3,text = str(items[3]))
            self.canvasMain.coords(self.id3, 90,200)

        def circle4(self):
            xval = 150
            yval = 180
            self.canvasMain.coords(self.circ4, xval,yval, xval+40, yval+40)
            self.canvasMain.coords(self.line4, 170,180,150,135)
            self.canvasMain.itemconfig(self.id4,text = str(items[4]))
            self.canvasMain.coords(self.id4, 170,200)

        def circle5(self):
            xval = 230
            yval = 180
            self.canvasMain.coords(self.circ5, xval,yval, xval+40, yval+40)
            self.canvasMain.coords(self.line5, 260,180,280,135)
            self.canvasMain.itemconfig(self.id5,text = str(items[5]))
            self.canvasMain.coords(self.id5, 250,200)

        def circle6(self):
            xval = 310
            yval = 180
            self.canvasMain.coords(self.circ6, xval,yval, xval+40, yval+40)
            self.canvasMain.coords(self.line6, 330,180,300,135)
            self.canvasMain.itemconfig(self.id6,text = str(items[6]))
            self.canvasMain.coords(self.id6, 330,200)

        def createCircle(self):
            if len(items) >= 1:#Index 0
                self.circle0()
            if len(items) >= 2:
                self.circle1()
            if len(items) >= 3:
                self.circle2()
            if len(items) >= 4:
                self.circle3()
            if len(items) >= 5:
                self.circle4()
            if len(items) >= 6:
                self.circle5()
            if len(items) >= 7:
                self.circle6()


        def removeCircle(self):
            if len(items) == 0:
                self.canvasMain.coords(self.id0, 0,0)
                self.canvasMain.coords(self.circ0, 0,0, 0, 0)  
            if len(items) == 1:
                self.canvasMain.coords(self.circ1, 0,0, 0, 0)  
                self.canvasMain.coords(self.line1,  0,0,0,0)
                self.canvasMain.coords(self.id1, 0,0)
                self.canvasMain.itemconfig(self.id0, text = str(items[0]))
            if len(items) == 2:
                self.canvasMain.coords(self.circ2, 0,0, 0, 0)  
                self.canvasMain.coords(self.line2,  0,0,0,0)
                self.canvasMain.coords(self.id2, 0,0)
                self.canvasMain.itemconfig(self.id0, text = str(items[0]))
                self.canvasMain.itemconfig(self.id1, text = str(items[1]))
            if len(items) == 3:
                self.canvasMain.coords(self.circ3, 0,0, 0, 0)
                self.canvasMain.coords(self.line3,  0,0,0,0)  
                self.canvasMain.coords(self.id3, 0,0)
                self.canvasMain.itemconfig(self.id0, text = str(items[0]))
                self.canvasMain.itemconfig(self.id1, text = str(items[1]))
                self.canvasMain.itemconfig(self.id2, text = str(items[2]))
            if len(items) == 4:
                self.canvasMain.coords(self.circ4, 0,0, 0, 0)
                self.canvasMain.coords(self.line4,  0,0,0,0)  
                self.canvasMain.coords(self.id4, 0,0)
                self.canvasMain.itemconfig(self.id0, text = str(items[0]))
                self.canvasMain.itemconfig(self.id1, text = str(items[1]))
                self.canvasMain.itemconfig(self.id2, text = str(items[2]))
                self.canvasMain.itemconfig(self.id3, text = str(items[3]))
            if len(items) == 5:
                self.canvasMain.coords(self.circ5, 0,0, 0, 0)
                self.canvasMain.coords(self.line5, 0,0,0,0)  
                self.canvasMain.coords(self.id5, 0,0)
                self.canvasMain.itemconfig(self.id0, text = str(items[0]))
                self.canvasMain.itemconfig(self.id1, text = str(items[1]))
                self.canvasMain.itemconfig(self.id2, text = str(items[2]))
                self.canvasMain.itemconfig(self.id3, text = str(items[3]))
                self.canvasMain.itemconfig(self.id4, text = str(items[4]))
            if len(items) == 6:
                self.canvasMain.coords(self.circ6, 0,0, 0, 0) 
                self.canvasMain.coords(self.line6, 0,0,0,0)   
                self.canvasMain.coords(self.id6, 0,0)
                self.canvasMain.itemconfig(self.id0, text = str(items[0]))
                self.canvasMain.itemconfig(self.id1, text = str(items[1]))
                self.canvasMain.itemconfig(self.id2, text = str(items[2]))
                self.canvasMain.itemconfig(self.id3, text = str(items[3]))
                self.canvasMain.itemconfig(self.id4, text = str(items[4]))
                self.canvasMain.itemconfig(self.id5, text = str(items[5]))

        #Function to retrieve user input from the textbox
        def getData(self):

            if len(items) < 7:
                num = eval(self.userInput.get())

                #Add Item to the back of the list
                items.append(num)

                #Fix heap(send larger number to the top)
                bubbleUp(len(items)-1)

                self.userInput.delete(0, 'end')

                self.createCircle()
            else:
                tkMessageBox.showinfo('!',"Heap is Full")

            #tkMessageBox.showinfo('result', str(len(items)))


        def removeData(self):
            if len(items) == 0:

                tkMessageBox.showinfo('!',"Heap is Empty")
            else:
                #Last item moved to the top
                items[0] = items[len(items)-1]

                #Remove last item
                items.pop()

                bubbleDown(0)

                self.removeCircle()

                #tkMessageBox.showinfo('result',items)

    #create an instance of the MyGUI class
    my_gui = MyGUI()
