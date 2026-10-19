from kivymd.app import MDApp
from kivy.lang import Builder
from kivy.uix.screenmanager import ScreenManager, Screen
from kivymd.uix.snackbar import Snackbar
import requests
from datetime import datetime

# --- BACKEND PART ---
class SOSManager:
    def get_location(self):
        return -29.9665, 30.8915
    def send_sos(self):
        lat, lon = self.get_location()
        print(f"SOS: https://maps.google.com/?q={lat},{lon} Time: {datetime.now()}")
        return True

# --- FRONTEND PART ---
KV = '''
ScreenManager:
    Screen:
        name: "home"
        MDBoxLayout:
            orientation: "vertical"
            MDTopAppBar:
                title: "Khusela - She is Safe"
            MDBoxLayout:
                orientation: "vertical"
                padding: 20
                spacing: 20
                MDLabel:
                    text: "Sawubona, Sibongile!"
                    font_style: "H4"
                    bold: True
                    size_hint_y: None
                    height: self.texture_size[1]
                MDCard:
                    size_hint_y: None
                    height: "180dp"
                    padding: 20
                    md_bg_color: "#6A1B9A"
                    MDBoxLayout:
                        orientation: "vertical"
                        MDRaisedButton:
                            text: "THUMELA SOS - SEND SOS"
                            md_bg_color: "#E53935"
                            size_hint_x: 1
                            on_release: app.trigger_sos()
'''

class KhuselaApp(MDApp):
    def build(self):
        self.sos = SOSManager()
        self.theme_cls.primary_palette = "DeepPurple"
        return Builder.load_string(KV)
    
    def trigger_sos(self):
        self.sos.send_sos()
        Snackbar(text="✅ SOS sent!").open()

KhuselaApp().run()
