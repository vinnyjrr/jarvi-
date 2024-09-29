# jarvi-
import speech_recognition as sr
import pyttsx3
import datetime

# Inicializa o reconhecedor de voz
recognizer = sr.Recognizer()

# Inicializa o sintetizador de voz
engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def listen():
    with sr.Microphone() as source:
        print("Aguardando comando...")
        audio = recognizer.listen(source)
        try:
            command = recognizer.recognize_google(audio, language='pt-BR')
            print(f"Você disse: {command}")
            return command.lower()
        except sr.UnknownValueError:
            print("Não consegui entender o que você disse.")
            return ""
        except sr.RequestError:
            print("Erro de conexão com o serviço de reconhecimento de voz.")
            return ""

def process_command(command):
    if "olá" in command:
        speak("Olá! Como posso ajudá-lo vinny?")
    elif "hora" in command:
        now = datetime.datetime.now()
        current_time = now.strftime("%H:%M")
        speak(f"A hora atual é {current_time}.")
    elif "sair" in command:
        speak("Até logo!")
        return False
    else:
        speak("Desculpe, não entendi o comando.")
    return True

def main():
    speak("Olá! Eu sou seu assistente virtual.")
    running = True
    while running:
        command = listen()
        running = process_command(command)

if __name__ == "__jarvis__":
    main()
