import sys
import math
from PyQt4 import QtCore, QtGui, uic
 
qtCreatorFile = "timetraq.ui" # Enter file here.
 
Ui_MainWindow, QtBaseClass = uic.loadUiType(qtCreatorFile)
rows = 0

class MyApp(QtGui.QMainWindow, Ui_MainWindow):
    
    ###BUTTON FUNCTION###
    def export(self):
        lines = []
        global rows
        for i in range(rows):
            for j in range(8):
                widg = self.timebars.itemAt(i).itemAt(j).widget()
                if(j != 0 and j%2 == 0):
                    lines.append(widg.cleanText())
                else:
                    lines.append(widg.text())
                lines.append(" ")
            lines.append("\n")
        
        try:
            fileName = QtGui.QFileDialog.getSaveFileName(self, "Save time", "",".txt")
            save = open(fileName, "w+")
            for l in lines:
                save.write(l)
            save.close()
        except:
            pass

    def addTime(self, a,t, grid):
            days = grid.itemAt(2).widget()
            hours = grid.itemAt(4).widget()
            mins = grid.itemAt(6).widget()

            if(t == 0):
                s = a + days.value()
                if(s < 0):
                    hours.setValue(0)
                    mins.setValue(0)
                days.setValue(s)
            if(t == 1):
                s = a + hours.value()
                if(days.value() == 0 and s < 0):
                    hours.setValue(0)
                else:
                    hours.setValue(s%24)
                    self.addTime(s//24, 0, grid)
            if(t == 2):
                s = a + mins.value()
                if(days.value() == 0 and hours.value() == 0 and s < 0):
                    mins.setValue(0)
                else:
                    mins.setValue(s%60)
                    self.addTime(s//60, 1, grid)

    def confirm(self):
    	global rows
        if(self.operation.currentIndex() == 0):
        	for i in range(rows):
        		gr = self.timebars.itemAt(i)
        		self.addTime(self.userTime.value(), self.units.currentIndex(), gr)
        else:
        	for i in range(rows):
        		gr = self.timebars.itemAt(i)
        		self.addTime(-self.userTime.value(), self.units.currentIndex(), gr)

    def addRow(self):
        global rows
        if rows > 10:
            alert = QtGui.QMessageBox()
            alert.setText("I think you have enough....")
            alert.exec_()
            return

        rows = rows + 1
        lbl = str(rows)
        newGrid = QtGui.QGridLayout()
        newGrid.setObjectName("timebox_"+lbl)
        
        ##name line
        newName = QtGui.QLabel("Name: ")
        newName.setObjectName("lblname_"+lbl)
        newLine = QtGui.QLineEdit()
        newLine.setObjectName("name_"+lbl)
        newLine.setGeometry(94,116,180,33)
        newLine.setSizePolicy(QtGui.QSizePolicy())
        
        ###new boxes
        newBox = [QtGui.QSpinBox(),QtGui.QSpinBox(),QtGui.QSpinBox()]
        newBox[0].setObjectName("uDays_"+lbl)
        newBox[1].setObjectName("uHours_"+lbl)
        newBox[2].setObjectName("uMinutes_"+lbl)

        newBox[0].setMaximum(999)
        newBox[1].setMaximum(23)
        newBox[2].setMaximum(59)

        ###new labels
        newlbl = [None] * 3
        newlbl[0] =  QtGui.QLabel("days")
        newlbl[0].setObjectName("uDays_"+lbl)
        newlbl[1] =  QtGui.QLabel("hours")
        newlbl[1].setObjectName("uHours_"+lbl)
        newlbl[2] =  QtGui.QLabel("minutes")
        newlbl[2].setObjectName("uMinutes_"+lbl)
       
        #add widgets to grid
        newGrid.addWidget(newName,0,0)
        newGrid.addWidget(newLine, 0, 1,1,2)
        newGrid.addWidget(newBox[0], 1, 0)
        newGrid.addWidget(newlbl[0], 1, 1)
        newGrid.addWidget(newBox[1], 1, 2)
        newGrid.addWidget(newlbl[1], 1, 3)
        newGrid.addWidget(newBox[2], 1, 4)
        newGrid.addWidget(newlbl[2], 1, 5)
        
        self.timebars.addLayout(newGrid)
        self.timebars.setAlignment(QtCore.Qt.AlignVCenter) 

    ###INIT###
    def __init__(self):
        QtGui.QMainWindow.__init__(self)
        Ui_MainWindow.__init__(self)
        self.setupUi(self)
        
        #buttons
        self.btnAdd.clicked.connect(self.addRow)
        self.btnConfirm.clicked.connect(self.confirm)
        self.btnExport.clicked.connect(self.export)

        #adds first timer
        self.addRow()

###MAIN###
if __name__ == "__main__":
    app = QtGui.QApplication(sys.argv)
    window = MyApp()
    window.show()
    sys.exit(app.exec_())





