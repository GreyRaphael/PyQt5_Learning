# PyQt5 Introduction

- [PyQt5 Introduction](#pyqt5-introduction)
  - [simple example with QtDesigner](#simple-example-with-qtdesigner)

## simple example with QtDesigner

Steps:
- in Anaconda Prompt: `designer`, open QtDesigner
- create `basic.ui` file in QtDesigner together with `res.qrc`
- `pyrcc5 -o res_rc.py res.qrc`: convert `.qrc` file to `.py` file
- `pyuic5 -o example.py basic.ui -x`: convert `.ui` file to `.py` file
- write signal-slot function to related `class`
- `python example.py`

```bash
# files
basic.ui
res.qrc
res_rc.py
example.py
```


```xml
<!-- basic.ui -->
<?xml version="1.0" encoding="UTF-8"?>
<ui version="4.0">
 <class>widgetWin</class>
 <widget class="QWidget" name="widgetWin">
  <property name="geometry">
   <rect>
    <x>0</x>
    <y>0</y>
    <width>322</width>
    <height>174</height>
   </rect>
  </property>
  <property name="windowTitle">
   <string>Form</string>
  </property>
  <property name="windowIcon">
   <iconset>
    <normaloff>favicon-5.ico</normaloff>favicon-5.ico</iconset>
  </property>
  <widget class="QLineEdit" name="lineEditUser">
   <property name="geometry">
    <rect>
     <x>100</x>
     <y>20</y>
     <width>191</width>
     <height>31</height>
    </rect>
   </property>
  </widget>
  <widget class="QLineEdit" name="lineEditPassword">
   <property name="geometry">
    <rect>
     <x>100</x>
     <y>70</y>
     <width>191</width>
     <height>31</height>
    </rect>
   </property>
   <property name="echoMode">
    <enum>QLineEdit::Password</enum>
   </property>
  </widget>
  <widget class="QLabel" name="label">
   <property name="geometry">
    <rect>
     <x>20</x>
     <y>30</y>
     <width>71</width>
     <height>16</height>
    </rect>
   </property>
   <property name="font">
    <font>
     <pointsize>10</pointsize>
    </font>
   </property>
   <property name="text">
    <string>Account(&amp;A)</string>
   </property>
   <property name="buddy">
    <cstring>lineEditUser</cstring>
   </property>
  </widget>
  <widget class="QLabel" name="label_2">
   <property name="geometry">
    <rect>
     <x>10</x>
     <y>80</y>
     <width>81</width>
     <height>16</height>
    </rect>
   </property>
   <property name="font">
    <font>
     <pointsize>10</pointsize>
    </font>
   </property>
   <property name="text">
    <string>Password(&amp;P)</string>
   </property>
   <property name="buddy">
    <cstring>lineEditPassword</cstring>
   </property>
  </widget>
  <widget class="QPushButton" name="buttonClear">
   <property name="geometry">
    <rect>
     <x>100</x>
     <y>120</y>
     <width>81</width>
     <height>31</height>
    </rect>
   </property>
   <property name="font">
    <font>
     <pointsize>10</pointsize>
    </font>
   </property>
   <property name="text">
    <string>Clear(&amp;C)</string>
   </property>
  </widget>
  <widget class="QPushButton" name="buttonLogin">
   <property name="geometry">
    <rect>
     <x>210</x>
     <y>120</y>
     <width>81</width>
     <height>31</height>
    </rect>
   </property>
   <property name="font">
    <font>
     <pointsize>10</pointsize>
    </font>
   </property>
   <property name="text">
    <string>OK(&amp;O)</string>
   </property>
  </widget>
 </widget>
 <resources>
  <include location="res.qrc"/>
 </resources>
 <connections>
  <connection>
   <sender>buttonLogin</sender>
   <signal>clicked()</signal>
   <receiver>widgetWin</receiver>
   <slot>check_login()</slot>
   <hints>
    <hint type="sourcelabel">
     <x>251</x>
     <y>140</y>
    </hint>
    <hint type="destinationlabel">
     <x>306</x>
     <y>139</y>
    </hint>
   </hints>
  </connection>
  <connection>
   <sender>buttonClear</sender>
   <signal>clicked()</signal>
   <receiver>widgetWin</receiver>
   <slot>clear_input()</slot>
   <hints>
    <hint type="sourcelabel">
     <x>142</x>
     <y>132</y>
    </hint>
    <hint type="destinationlabel">
     <x>71</x>
     <y>138</y>
    </hint>
   </hints>
  </connection>
 </connections>
 <slots>
  <slot>check_login()</slot>
  <slot>clear_input()</slot>
 </slots>
</ui>
```

```xml
<!-- res.qrc -->
<RCC>
  <qresource prefix="winIcon">
    <file>favicon-5.ico</file>
  </qresource>
</RCC>
```

```py
# example.py
# -*- coding: utf-8 -*-

# Form implementation generated from reading ui file 'basic.ui'
#
# Created by: PyQt5 UI code generator 5.9.2
#
# WARNING! All changes made in this file will be lost!

from PyQt5 import QtCore, QtGui, QtWidgets

class Ui_widgetWin(object):
    def setupUi(self, widgetWin):
        widgetWin.setObjectName("widgetWin")
        widgetWin.resize(322, 174)
        icon = QtGui.QIcon()
        icon.addPixmap(QtGui.QPixmap("favicon-5.ico"), QtGui.QIcon.Normal, QtGui.QIcon.Off)
        widgetWin.setWindowIcon(icon)
        self.lineEditUser = QtWidgets.QLineEdit(widgetWin)
        self.lineEditUser.setGeometry(QtCore.QRect(100, 20, 191, 31))
        self.lineEditUser.setObjectName("lineEditUser")
        self.lineEditPassword = QtWidgets.QLineEdit(widgetWin)
        self.lineEditPassword.setGeometry(QtCore.QRect(100, 70, 191, 31))
        self.lineEditPassword.setEchoMode(QtWidgets.QLineEdit.Password)
        self.lineEditPassword.setObjectName("lineEditPassword")
        self.label1 = QtWidgets.QLabel(widgetWin)
        self.label1.setGeometry(QtCore.QRect(20, 30, 71, 16))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.label1.setFont(font)
        self.label1.setObjectName("label1")
        self.label2 = QtWidgets.QLabel(widgetWin)
        self.label2.setGeometry(QtCore.QRect(10, 80, 81, 16))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.label2.setFont(font)
        self.label2.setObjectName("label2")
        self.buttonClear = QtWidgets.QPushButton(widgetWin)
        self.buttonClear.setGeometry(QtCore.QRect(100, 120, 81, 31))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.buttonClear.setFont(font)
        self.buttonClear.setObjectName("buttonClear")
        self.buttonLogin = QtWidgets.QPushButton(widgetWin)
        self.buttonLogin.setGeometry(QtCore.QRect(210, 120, 81, 31))
        font = QtGui.QFont()
        font.setPointSize(10)
        self.buttonLogin.setFont(font)
        self.buttonLogin.setObjectName("buttonLogin")
        self.label1.setBuddy(self.lineEditUser)
        self.label2.setBuddy(self.lineEditPassword)

        self.retranslateUi(widgetWin)
        self.buttonClear.clicked.connect(self.lineEditUser.clear)
        self.buttonClear.clicked.connect(self.lineEditPassword.clear)
        self.buttonLogin.clicked.connect(self.check_login)
        QtCore.QMetaObject.connectSlotsByName(widgetWin)

    def retranslateUi(self, widgetWin):
        _translate = QtCore.QCoreApplication.translate
        widgetWin.setWindowTitle(_translate("widgetWin", "Form"))
        self.label1.setText(_translate("widgetWin", "Account(&A)"))
        self.label2.setText(_translate("widgetWin", "Password(&P)"))
        self.buttonClear.setText(_translate("widgetWin", "Clear(&C)"))
        self.buttonLogin.setText(_translate("widgetWin", "OK(&O)"))

    def check_login(self):
        if self.lineEditUser.text()=="gewei" and self.lineEditPassword.text()=="123456":
            # login success
            widgetWin.close()
            
            d=QtWidgets.QDialog()
            d.setWindowTitle('Congratulation!')
            d.setWindowFlags(QtCore.Qt.Dialog | QtCore.Qt.CustomizeWindowHint | QtCore.Qt.WindowTitleHint|QtCore.Qt.WindowCloseButtonHint)

            d.resize(300, 100)
            l1=QtWidgets.QLabel(d)
            l1.move(10, 10)
            l1.setText('Login Success!')
            d.setWindowModality(QtCore.Qt.ApplicationModal)
            d.exec_()

        else:
            # login fail
            QtWidgets.QMessageBox.information(widgetWin, "Information", 'Password Wrong!')

import res_rc

if __name__ == "__main__":
    import sys
    app = QtWidgets.QApplication(sys.argv)
    widgetWin = QtWidgets.QWidget()
    ui = Ui_widgetWin()
    ui.setupUi(widgetWin)
    widgetWin.show()
    sys.exit(app.exec_())
```
