# Ruffier's health_test
В этом тесте идет проверка сердечно-сосудистой системы человека
При физических нагрузках и оценка эффективности этой работы.
Первое окно это обьясняет вам про этот тест и что в нем нужно делать,
а также это предупреждение, что в процесе этого теста у вас может почуствовать шум в ушах или головокружение то этот тест нужно прекратить и обратиться к врачу
![1](https://github.com/Aslan7002/Health_test/assets/143867439/19c97345-8365-4461-848b-33d96fb83b3b)
Во втором окне начинается сам тест.
В нем вам можно написать ваше имя и ВАЖНО написать ваш возраст ведь это повлияет на результат.
![2](https://github.com/Aslan7002/Health_test/assets/143867439/06fe3a78-05d6-4f32-8e35-82ce9cbb4ff7)
Действие 1) Как будите готовы нажмите на "Начать первый тест" и замерьте свой пульс в течении 15 секунд
Действие 2) После вам за 45 секунд нужно сделать 30 приседаний.
Действие 3) Вы нажимаете "Начать финальный тест" и измеряете свой пульс за первые и последние 15 секунд. Они выделены зеленым цветом
Все результаты записываете в нужные окошки и после выполнения нажимайте "Отравить результаты"
![3](https://github.com/Aslan7002/Health_test/assets/143867439/58f25df5-efa7-437a-a903-4fc91a6b0c76)
Снизу будет написана ваша работо способность сердца и стоит ли пойти к врачу.



Я проверял этот проект по специальному листу
![cheack](https://github.com/Aslan7002/Health_test/assets/143867439/a1d70aab-eb41-407d-bb79-d7f268912b00)
![cheack_2](https://github.com/Aslan7002/Health_test/assets/143867439/ec8621eb-2a4c-405e-a6e6-faf783897971)

Сам код:
#1)
from PyQt5.QtCore import Qt, QTimer, QTime, QLocale
from PyQt5.QtGui import QDoubleValidator, QIntValidator, QFont 
from PyQt5.QtWidgets import (
        QApplication, QWidget,
        QHBoxLayout,QVBoxLayout, QGridLayout,
        QGroupBox, QRadioButton,
        QPushButton, QLabel, QListWidget, QLineEdit)

from instr import *
from second_win import *

class MainWin(QWidget):
    def __init__(self):
        super().__init__()
        self.set_appear()
        self.initUI()
        self.connects()
        self.show()
    def initUI(self):
        self.btn_next = QPushButton(txt_next)
        self.hello_text = QLabel(txt_hello)
        self.instruction = QLabel(txt_instruction)
        self.layout = QVBoxLayout()
        self.layout.addWidget(self.hello_text, alignment = Qt.AlignLeft)
        self.layout.addWidget(self.instruction, alignment = Qt.AlignCenter)
        self.layout.addWidget(self.btn_next, alignment = Qt.AlignCenter)
        self.setLayout(self.layout)

    def next_click(self):
        self.tw = TestWin()
        self.hide()

    def connects(self):
        self.btn_next.clicked.connect(self.next_click)

    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_width, win_height)
        self.move(win_x, win_y)


app = QApplication([])
mw = MainWin()
app.exec_()
#2)
from PyQt5.QtCore import Qt, QTimer, QTime, QLocale
from PyQt5.QtGui import QDoubleValidator, QIntValidator, QFont
from PyQt5.QtWidgets import (
        QApplication, QWidget,
        QHBoxLayout, QVBoxLayout,QGridLayout,
        QGroupBox, QRadioButton,
        QPushButton, QLabel, QListWidget, QLineEdit)

from instr import*
from final_win import *

class Experiment():
    def __init__(self, age, test1, test2, test3):
        self.age = age
        self.t1 = test1
        self.t2 = test2
        self.t3 = test3

class TestWin(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()
        self.connects()
        self.set_appear()
        self.show()
    
    def set_appear(self):
        self.setWindowTitle(txt_title)
        self.resize(win_width, win_height)
        self.move(win_x, win_y)        

    def initUI(self):
        self.btn_next = QPushButton(txt_sendresults, self)
        self.btn_test1 = QPushButton(txt_starttest1, self)
        self.btn_test2 = QPushButton(txt_starttest2, self)
        self.btn_test3 = QPushButton(txt_starttest3, self)

        self.text_name = QLabel(txt_name)
        self.text_age = QLabel(txt_age)
        self.text_test1 = QLabel(txt_test1)
        self.text_test2 = QLabel(txt_test2)
        self.text_test3 = QLabel(txt_test3)
        self.text_timer = QLabel(txt_timer)
        self.text_timer.setFont(QFont("Times", 36, QFont.Bold))


        self.line_name = QLineEdit(txt_hintname)
        self.line_age = QLineEdit(txt_hintage)
        self.line_test1 = QLineEdit(txt_hinttest1)
        self.line_test2 = QLineEdit(txt_hinttest2)
        self.line_test3 = QLineEdit(txt_hinttest3)

        self.l_line = QVBoxLayout()
        self.r_line = QVBoxLayout()
        self.h_line = QVBoxLayout()
        self.r_line.addWidget(self.text_timer, alignment = Qt.AlignCenter)
        self.l_line.addWidget(self.text_name, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.line_name, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.text_age, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.line_age, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.text_test1, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.btn_test1, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.line_test1, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.text_test2, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.btn_test2, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.line_test2, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.text_test3, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.btn_test3, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.line_test3, alignment = Qt.AlignLeft)
        self.l_line.addWidget(self.btn_next, alignment = Qt.AlignCenter)
        self.h_line.addLayout(self.l_line)
        self.h_line.addLayout(self.r_line)
        self.setLayout(self.h_line)

    def next_click(self):
        self.hide()
        self.exp = Experiment(int(self.line_age.text()), self.line_test1.text(), self.line_test2.text(), self.line_test2.text())
        self.fw = FinalWin(self.exp)

    def timer_test(self):
        global time
        time = QTime(0, 0, 15)
        self.timer = QTimer()
        self.timer.timeout.connect(self.timer1Event)
        self.timer.start(1000)

    def timer_sits(self):
        global time
        time = QTime(0, 0, 30)
        self.timer = QTimer()
        self.timer.timeout.connect(self.timer2Event)
        self.timer.start(1500)       
    
    def timer_final(self):
        global time
        time = QTime(0, 1, 0)
        self.timer = QTimer()
        self.timer.timeout.connect(self.timer3Event)
        self.timer.start(1000)

    def timer1Event(self):
        global time
        time = time.addSecs(-1)
        self.text_timer.setText(time.toString("hh:mm:ss"))
        self.text_timer.setFont(QFont("Times", 36, QFont.Bold))
        self.text_timer.setStyleSheet("color: rgb(0,0,0)")
        if time.toString("hh:mm:ss") == "00:00:00":
            self.timer.stop()

    def timer2Event(self):
        global time
        time =time.addSecs(-1)
        self.text_timer.setText(time.toString("hh:mm:ss")[6:8])
        self.text_timer.setFont(QFont("Times", 36, QFont.Bold))
        self.text_timer.setStyleSheet("color: rgb(0,0,0)")
        if time.toString("hh:mm:ss") == "00:00:00":
            self.timer.stop()

    def timer3Event(self):
        global time
        time = time.addSecs(-1)
        self.text_timer.setText(time.toString("hh:mm:ss"))
        if int(time.toString("hh:mm:ss")[6:8]) >= 45:
            self.text_timer.setStyleSheet("color: rgb(0,255,0)")
        elif int(time.toString("hh:mm:ss")[6:8]) <= 15:
            self.text_timer.setStyleSheet("color: rgb(0,255,0)")
        else:
            self.text_timer.setStyleSheet("color: rgb(0, 0, 0)")
        self.text_timer.setFont(QFont("Times", 36, QFont.Bold))
        if time.toString("hh:mm:ss") == "00:00:00":
            self.timer.stop()

    def connects(self):
        self.btn_next.clicked.connect(self.next_click)
        self.btn_test1.clicked.connect(self.timer_test)
        self.btn_test2.clicked.connect(self.timer_sits)
        self.btn_test3.clicked.connect(self.timer_final)  

#3)
from PyQt5.QtCore import Qt, QTimer, QTime, QLocale
from PyQt5.QtGui import QDoubleValidator, QIntValidator, QFont
from PyQt5.QtWidgets import (
        QApplication, QWidget,
        QHBoxLayout,QVBoxLayout, QGridLayout,
        QGroupBox, QRadioButton,
        QPushButton, QLabel, QListWidget, QLineEdit)

from instr import *


class FinalWin(QWidget):
    def __init__(self, exp):
        super().__init__()
        self.exp = exp
        self.initUI()
        self.set_appear()
        self.show()


    def results(self):
        if self.exp.age < 7:
            self.index = 0
            return "нет данных для этого возраста"
        self.index = (4 * (int(self.exp.t1) + int(self.exp.t2) + int(self.exp.t3) - 200) / 10)
        if self.exp.age == 7 or self.exp.age == 8:
            if self.index >= 21:
                return txt_res1
            elif self.index < 21 and self.index >= 17:
                return txt_res2
            elif self.index < 17 and self.index >= 12:
                return txt_res3
            elif self.index < 12 and self.index >= 6.5:
                return txt_res4
            else:
                return txt_res5
            
        if self.exp.age == 9 or self.exp.age == 10:
            if self.index >= 19.5:
                return txt_res1
            elif self.index < 19.5 and self.index >= 15.5:
                return txt_res2
            elif self.index < 15.5 and self.index >= 10.5:
                return txt_res3
            elif self.index < 10.5 and self.index >= 5:
                return txt_res4
            else:
                return txt_res5

        if self.exp.age == 11 or self.exp.age == 12:
            if self.index > 18:
                return txt_res1
            elif self.index < 18 and self.index >= 14:
                return txt_res2
            elif self.index < 14 and self.index >= 9:
                return txt_res3
            elif self.index < 9 and self.index >= 3.5:
                return txt_res4
            else:
                return txt_res5
        
        if self.exp.age == 13 or self.exp.age == 14:
            if self.index >= 16.5:
                return txt_res1
            elif self.index < 16.5 and self.index >= 12.5:
                return txt_res2
            elif self.index < 12.5 and self.index >= 7.5:
                return txt_res3
            elif self.index < 7.5 and self.index >= 2:
                return txt_res4
            else:
                return txt_res5

        if self.exp.age >= 15:
            if self.index >= 15:
                return txt_res1
            elif self.index < 15 and self.index >= 11:
                return txt_res2
            elif self.index < 11 and self.index >= 6:
                return txt_res3
            elif self.index < 6 and self.index >= 0.5:
                return txt_res4
            else:
                return txt_res5

    def initUI(self):
        self.work_text = QLabel(txt_workheart + self.results())
        self.index_text = QLabel(txt_index + str(self.index))


        self.layout_line = QVBoxLayout()
        self.layout_line.addWidget(self.index_text, alignment = Qt.AlignCenter)
        self.layout_line.addWidget(self.work_text, alignment = Qt.AlignCenter)
        self.setLayout(self.layout_line)

    
    def set_appear(self):
            self.setWindowTitle(txt_finalwin)
            self.resize(win_width,win_height)
            self.move(win_x, win_y)

# Вот тут хранятся все надписи
from PyQt5.QtCore import QTime
win_x, win_y = 200, 100
win_width, win_height = 1000, 600

txt_hello = 'Добро пожаловать в программу по определению состояния здоровья!'
txt_next = 'Начать'
txt_instruction = ('Данное приложение позволит вам с помошью теста Руфье провести первичную диагностику вашего здоровья.\n'
                   'Проба Руфье предоставляет собой нагрузной комплексб предназначенный для оценки работоспособности сердца при физической нагрузке.\n'
                   'У испытуемого, находящегося в положении лёжа на спине в течении 5 мин, определяют частотупульса за 15 секунд;\n'
                   'затем в течении 45 секунд испытуемый выполняет 30 приседаний.\n'
                   'После окончания нагрузки испетуемый ложится, и у него вновь подчитывается за первые 15 секунд,\n'
                   'а потом - за последние 15 секунд первой минуты периода восстановления.\n'
                   'Важно! Если в процессе проведения испытания вы почуствуете себя плохо(появится головокружение, нум в\n'
                   'ушах, сильная одышка и др.), то тест необходимо прервать и обратиться к врачу.')
txt_title = 'Здоровье'
txt_name = 'Введите Ф.И.О.:'
txt_hintname = "Ф.И.О."
txt_hintage = "0"
txt_test1 = 'Ложитесь на спину и замерьте пульс за 15 секунд. Нажмите кнопку "Начать первый тест", чтобы запустить таймер.\nРезультат запишите в нужном поле.'
txt_test2 = 'Выполните 30 пресиданий за 45 секунд. Для этого нажмите кнопку "Начать делать пресидания",\nчтобы запустить счётчик пресиданий.'
txt_test3 = '''Ляжте на спину и замерьте пульса сначала за первые 15 секунд минуты, затем за последние 15 секунд.\nНажмите кнопку
"Начать финальный тест", чтобы запустить таймер. \nЗёленым обозначены секунды в течение которых необходимо \nпроводить измерения, черным - 
секунды без замера пульсаций. Результаты запишите в соответству поля.'''
txt_sendresults = 'Отправить результаты'
txt_hinttest1 = '0'
txt_hinttest2 = '0'
txt_hinttest3 = '0'
txt_starttest1 = 'Начать первый тест'
txt_starttest2 = 'Начать делать пресидания'
txt_starttest3 = 'Начать финальный тест'
time = QTime(0,0,15)
txt_timer =  time.toString("hh:mm:ss")
txt_age = 'Полных лет'
txt_finalwin = 'Результаты'
txt_index = 'Индекс Руфье:'
txt_workheart = 'Работоспособность сердца:'
txt_res1 = "низкая. Срочно обратитесь к врачу!"
txt_res2 = "удволитворительная.Обратитесь к врачу!"
txt_res3 = "средняя. Возможно, стоит дополнительно обследоваться у врача."
txt_res4 = "выше среднего"
txt_res5 = "высокая"
