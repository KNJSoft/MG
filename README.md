# MG
# chiffrement de hill en utilisant Python et kivy
from kivy.app import App
from kivy.metrics import dp
from kivy.properties import StringProperty
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label

liste_caracter = ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s",
                  "t",
                  "u", "v", "w", "x", "y", "z", "-1"]

liste_alphabetique = {0: "a", 1: "b", 2: "c", 3: "d", 4: "e", 5: "f", 6: "g", 7: "h", 8: "i", 9: "j", 10: "k",
                      11: "l", 12: "m", 13: "n", 14: "o", 15: "p", 16: "q", 17: "r", 18: "s", 19: "t", 20: "u",
                      21: "v", 22: "w",
                      23: "x", 24: "y", 25: "z", -1: ' '}


class Hill(BoxLayout):
    messageChiffre = StringProperty()

    def chiffre(self):
        a = int(self.ids.c_a.text)
        b = int(self.ids.c_b.text)
        c = int(self.ids.c_c.text)
        d = int(self.ids.c_d.text)

        _message = self.ids.message_non_chiffre.text
        # _message_chiffre = self.ids.Message_chiffre

        phras = _message
        phrase = phras.split(" ")

        mot = []
        premier = 0
        deuxieme = 0
        message_1 = None
        message_2 = None
        mot_chiffre = []
        message_code = "rien"

        print(phrase)
        for i in phrase:
            for u in i:
                mot.append(u)

        print(mot)
        mot_int = len(mot)
        i = 0
        while not i == mot_int:
            index = i
            try:
                c_1 = mot[index]
                if c_1 == mot[index]:
                    mot.remove(c_1)
            except:
                break
            try:
                c_2 = mot[index]
                if c_2 == mot[index]:
                    mot.remove(c_2)
            except IndexError:
                c_2 = -1
            i += i
            mot_int -= i

            for car in range(len(liste_caracter)):
                try:
                    if c_1 == liste_caracter[car]:
                        premier = int(car)
                    if c_2 == -1:
                        message_code = (a * premier) + (c * premier)

                        if message_code >= 26:
                            message_code %= 26
                    else:
                        if c_2 == liste_caracter[car]:
                            deuxieme = int(car)

                    message_1 = (a * premier) + (b * deuxieme)
                    message_2 = (c * premier) + (d * deuxieme)

                    if message_1 >= 26:
                        message_1 %= 26
                    if message_2 >= 26:
                        message_2 %= 26
                except IndexError:
                    break
            if not message_code == "rien":
                mot_chiffre.append(liste_alphabetique[message_code])
                break
            mot_chiffre.append(liste_alphabetique[message_1])
            mot_chiffre.append(liste_alphabetique[message_2])

        word = ''
        for i in mot_chiffre:
            word += i
        print(word)

        self.messageChiffre = word


class MonApp(App):
    pass


MonApp().run()
