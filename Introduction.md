# PyQt5 Introduction

- [PyQt5 Introduction](#pyqt5-introduction)
  - [simple example with QtDesigner](#simple-example-with-qtdesigner)
  - [PyQt5 with matplotlib](#pyqt5-with-matplotlib)
  - [PyQt5 Multiple windows](#pyqt5-multiple-windows)

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
import pymongo

CLI=pymongo.MongoClient('mongodb://grey:xxxxxx@localhost:27017')
COLLECTION=CLI.irradiation.data

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
        result=COLLECTION.find_one({'name_id': self.lineEditUser.text()})
        if result:
            # username in database
            if result['name_id']==self.lineEditPassword.text():
                # password right
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
                # password wrong
                QtWidgets.QMessageBox.information(widgetWin, "Information", "Password Wrong!")
        else:
            # username not in database
            QtWidgets.QMessageBox.information(widgetWin, "Information", "User not exist!")

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

## PyQt5 with matplotlib

```py
import random
import sys
from PyQt5 import QtWidgets
import matplotlib.pyplot as plt 

plt.ion()

class MainWindow(QtWidgets.QMainWindow):
    def __init__(self):
        super().__init__()
        self.move(100, 100)
        self.btn=QtWidgets.QPushButton("OK", self)
        self.btn.clicked.connect(self.update_plot)
        self.show()

    def update_plot(self):
        plt.cla()
        plt.plot(range(10), random.sample(range(100), 10), 'ro-')
        plt.show()

if __name__ == "__main__":
    app = QtWidgets.QApplication(sys.argv)
    w = MainWindow()
    app.exec_()
```

## PyQt5 Multiple windows

目标：窗口1实现button, tableview; 窗口2实现tableview右键编辑功能; 两个窗口数据共享
> ![](img/multi-win01.jpg)

```bash
main.py
models.py
MongoOperation.py
```

```py
# main.py
import sys
from PyQt5 import QtWidgets, QtGui, QtCore
import MongoOperation
from models import MyModel


class AnotherWindow(QtWidgets.QWidget):
    def __init__(self, model):
        self._model=model
        super().__init__()
        self.move(800, 100)
        layout=QtWidgets.QVBoxLayout()
        self.tableView=QtWidgets.QTableView()
        layout.addWidget(self.tableView)
        self.setLayout(layout)

        self.tableView.setModel(self._model)
        self.tableView.setContextMenuPolicy(QtCore.Qt.CustomContextMenu)
        self.tableView.customContextMenuRequested.connect(self.context_menu)

    def context_menu(self):
        menu=QtWidgets.QMenu()
        # context_menu: add
        menu_add=menu.addAction('+ Add New Row')
        menu_add.triggered.connect(self.add_action)

        # context_menu: add document(dictionary)
        menu_add_doc=menu.addAction('+ Add Document(Dictionary)')
        menu_add_doc.triggered.connect(self.add_doc_action)

        # context_menu: delete
        selected_indexes=self.tableView.selectedIndexes()
        if selected_indexes:
            menu_del=menu.addAction('- Delete Selected Rows')
            menu_del.triggered.connect(lambda : self._model.custom_delete_rows(selected_indexes))
        

        cursor=QtGui.QCursor()
        menu.exec_(cursor.pos())

    def add_action(self):
        self._model.custom_add_row()
        self.tableView.scrollToBottom()

    def add_doc_action(self):
        result, ok=QtWidgets.QInputDialog.getMultiLineText(self, 'Input Dictionary', 'Add Dictionary', '{\n\n\n\n}')
        if ok:
            try:
                data=eval(result)
            except Exception as e:
                msgBox=QtWidgets.QMessageBox(QtWidgets.QMessageBox.Warning, 'Failed', 'Must Add Valid Dictionary, Try Again!')
                msgBox.exec_()
            else:
                if isinstance(data, dict):

                    msgBox=QtWidgets.QMessageBox(QtWidgets.QMessageBox.Information, 'Success', 'Add Document Success!')
                    msgBox.exec_()

                    self._model.custom_add_document(data)
                    self.tableView.scrollToBottom()
                    # 刷新模型，更改表结构
                    self._model.beginResetModel()
                    self._model.endResetModel()
                else:
                    msgBox=QtWidgets.QMessageBox(QtWidgets.QMessageBox.Warning, 'Failed', 'Must Add Dictionary, Try Again!')
                    msgBox.exec_()



class MainWindow(QtWidgets.QWidget):
    def __init__(self):
        super().__init__()
        self.w = None  # No external window yet.

        layout=QtWidgets.QVBoxLayout()
        self.btn1=QtWidgets.QPushButton('Go to AnotherWindow')
        self.tableV=QtWidgets.QTableView()
        layout.addWidget(self.btn1)
        layout.addWidget(self.tableV)
        self.setLayout(layout)

        self.btn1.clicked.connect(self.show_new_window)
        
        data_list=MongoOperation.get_data_list()
        self._model=MyModel(data_list)
        self.tableV.setModel(self._model)


    def show_new_window(self):
        if self.w is None:
            self.w = AnotherWindow(self._model)
            self.w.show()
        else:
            # # no discard window
            # self.w.hide()

            # discard window
            self.w.close()  # Close window.
            self.w = None  # Discard reference.

if __name__ == "__main__":
    app = QtWidgets.QApplication(sys.argv)
    w = MainWindow()
    w.show()
    app.exec_()
```

```py
# models.py
from PyQt5 import QtCore, QtGui
import MongoOperation


class MyModel(QtCore.QAbstractTableModel):
    def __init__(self, dict_list):
        super().__init__()
        self._data=dict_list
        self._columns=None

    def rowCount(self, index):
        return len(self._data)

    def columnCount(self, index):
        self._columns=[]
        for d in self._data:
            for k in d.keys():
                if k not in self._columns:
                    self._columns.append(k)

        return len(self._columns)

    def headerData(self, section, orientation, role):
        if role==QtCore.Qt.DisplayRole:
            if orientation==QtCore.Qt.Horizontal:
                return self._columns[section]
            elif orientation==QtCore.Qt.Vertical:
                return section+1

    def flags(self, index):
        if index.column()==0:
            return QtCore.Qt.ItemIsEnabled | QtCore.Qt.ItemIsSelectable
        else:
            return QtCore.Qt.ItemIsEnabled | QtCore.Qt.ItemIsSelectable | QtCore.Qt.ItemIsEditable

    def data(self, index, role):
        if index.isValid():
            # print(role)
            r=index.row()
            c=index.column()
            column_name=self._columns[c]
            value=self._data[r].get(column_name)
            if role==QtCore.Qt.DisplayRole or role==QtCore.Qt.EditRole:
                if value:
                    return str(value)
                else:
                    return 'N/A'
            
            if role==QtCore.Qt.ForegroundRole:
                if not value:
                    return QtGui.QColor('#aaa')

    def setData(self, index, value, role):
        if index.isValid():
            r=index.row()
            current_row=self._data[r]
            c=index.column()
            column_name=self._columns[c]
            
            try:
                real_value=eval(value)
            except Exception as e:
                if value=='N/A' or value=='':
                    current_row.pop(column_name, None)
                else:
                    current_row[column_name]=value
            else:
                current_row[column_name]=real_value
            
            print(current_row)
            ok=MongoOperation.update_row(current_row)
            if ok:
                self.dataChanged.emit(index, index, [QtCore.Qt.DisplayRole,])
                return True
            else:
                return False
        else:
            return False

    def custom_add_row(self):
        row_count=len(self._data)
        self.beginInsertRows(QtCore.QModelIndex(), row_count, row_count)
        empty_row={column_name:None for column_name in self._columns if column_name !='_id'}
        doc_id=MongoOperation.insert_row(empty_row)
        new_row=MongoOperation.get_row(doc_id)
        self._data.append(new_row)
        self.endInsertRows()
        # 末端添加行数据不会引起表结构改变；
        # self.beginResetModel()
        # self.endResetModel()        
        return True

    def custom_add_document(self, row):
        row_count=len(self._data)
        self.beginInsertRows(QtCore.QModelIndex(), row_count, row_count)

        doc_id=MongoOperation.insert_row(row)
        new_row=MongoOperation.get_row(doc_id)
        self._data.append(new_row)
        
        self.endInsertRows()
        # 加入dictionary可能引入表结构改变；更新表结构
        self.beginResetModel()
        self.endResetModel()        
        return True

    def custom_delete_rows(self, selected_indexes):
        row_indexes=[index.row() for index in selected_indexes]
        unique_row_indexes=sorted(set(row_indexes), reverse=True)

        self.beginRemoveRows(QtCore.QModelIndex(),unique_row_indexes[-1], unique_row_indexes[0])

        doc_ids=[self._data[row_index]['_id'] for row_index in unique_row_indexes]
        MongoOperation.delete_rows(doc_ids)
        
        # print(unique_row_indexes)
        for index in unique_row_indexes:
            self._data.pop(index)

        self.endRemoveRows()
        # 删除行数据可能引起表结构改变；更新表结构
        self.beginResetModel()
        self.endResetModel()
        return True
```

```py
# MongoOperation.py
import pymongo
from bson import ObjectId

CLI=pymongo.MongoClient('mongodb://grey:xxxxxx@localhost:27017')
COLLECTION=CLI.irradiation.data

def get_data_list():
    # return list(COLLECTION.find().limit(number))
    return list(COLLECTION.find())

def get_row(doc_id):
    row=COLLECTION.find_one({'_id':ObjectId(doc_id)})
    return row

def update_row(row):
    doc_id=ObjectId(row['_id'])
    result=COLLECTION.replace_one({'_id':doc_id}, row, upsert=True)
    return result.acknowledged

def insert_row(row):
    result=COLLECTION.insert_one(row)
    return result.inserted_id

def delete_rows(doc_ids):
    for doc_id in doc_ids:
        COLLECTION.delete_one({'_id': doc_id})
```