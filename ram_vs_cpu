"""
github.com/blalyasar
medium.com/@blalyasar
kaggle.com/blalyasar
twitter.com/blalyasar
blalyasar@gmail.com

"""

from PyQt5.QtWidgets import QProgressBar
from PyQt5.QtWidgets import QApplication
from PyQt5.QtWidgets import QVBoxLayout
from PyQt5.QtWidgets import QHBoxLayout
from PyQt5.QtWidgets import QWidget
from PyQt5.QtWidgets import QLabel
from PyQt5.QtWidgets import QDial
from PyQt5.QtCore import QTimer
from PyQt5.QtCore import QThread 
from PyQt5.QtCore import pyqtSignal
from PyQt5.QtCore import pyqtSlot
from PyQt5.QtCore import Qt
from PyQt5 import QtGui
import platform
import psutil
import sys


class AppDemo(QWidget):

    def __init__(self):
        super().__init__()
        self.setWindowTitle(platform.system()+ " Hello "+platform.node())
        self.resize(400, 400)

        cpulabel = QLabel("CPU KULLANIM BİLGİLERİ")
        cpulabelname = QLabel(platform.processor())
        print("System: " + platform.processor())

        ramlabel = QLabel("RAM KULLANIM BİLGİLERİ")
        self.ramlabelpercent = QLabel("RAM KULLANIM BİLGİLERİ")


        cpulabel.setAlignment(Qt.AlignCenter)
        cpulabelname.setAlignment(Qt.AlignCenter)
        ramlabel.setAlignment(Qt.AlignCenter)
        self.ramlabelpercent.setAlignment(Qt.AlignCenter)

        self.progressBar = QProgressBar(self)

        
        self.progressBar.setTextVisible(True)

        self.progressBar.setMaximum(100)
        self.progressBar.setValue(0)

        self.dial = QDial(self)

        self.dial.setMinimum(0)
        self.dial.setMaximum(100)
        #çizgiler
        self.dial.setNotchesVisible(True)

        self.progressBar1 = QProgressBar(self)
        self.progressBar1.setTextVisible(True)
        

        self.progressBar1.setValue(0)
        self.progressBar1.setMaximum(100)

        self.dial1 = QDial(self)

        self.dial1.setMaximum(100)
        self.dial1.setMinimum(0)

        self.dial1.setNotchesVisible(True)


        layout0 = QHBoxLayout()
        layout1 = QHBoxLayout()
        layout2 = QVBoxLayout()

        layout0.addWidget(self.progressBar)
        layout0.addWidget(self.dial)

        layout1.addWidget(self.progressBar1)
        layout1.addWidget(self.dial1)


        layout2.addWidget(cpulabel)
        layout2.addWidget(cpulabelname)
        layout2.addLayout(layout0)
        layout2.addWidget(ramlabel)
        layout2.addWidget(self.ramlabelpercent)
        layout2.addLayout(layout1)
        self.setLayout(layout2)

        timer = QTimer(
            self,
            timeout=self.tick_update,
            interval=0,
        )
        timer.start()


    @pyqtSlot()
    def tick_update(self):

        self.dial.setValue(int(psutil.cpu_percent(interval=1)))
        self.progressBar.setValue(int(psutil.cpu_percent(interval=1)))

      
        mem = psutil.virtual_memory()
        # THRESHOLD = 100 * 1024 * 1024  # 100MB
        
        print(str(mem.total/ (1000*1024*1024)) + " GB")
        
        print(str(mem.available / (1000*1024*1024))+" GB")
       
        print(str(mem.used / (1000*1024*1024))+" GB")

        self.ramlabelpercent.setText(str(round(mem.used / (1000*1024*1024),2))+" GB"+"/"+
                                    str(round(mem.total/ (1000*1024*1024),2)) + " GB "+ 
                                    "%"+str(round(mem.percent)))

        self.dial1.setValue(int(mem.percent))
        self.progressBar1.setValue(int(mem.percent))

app = QApplication(sys.argv)
demo = AppDemo()
demo.show()
sys.exit(app.exec_())   
