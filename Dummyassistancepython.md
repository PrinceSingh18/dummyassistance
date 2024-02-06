import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import smtplib

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wish_me():
    hour = datetime.datetime.now().hour
    if 0 <= hour < 12:
        speak("hey Prince, Good morning!")
    elif 12 <= hour < 18:
        speak("hey Prince, Good afternoon!")
    else:
        speak("hey Prince, Good evening!")


def take_command():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening....")
        recognizer.pause_threshold = 1
        audio = recognizer.listen(source)

    try:
        print("Recognizing...")
        query = recognizer.recognize_google(audio, language='en-in')
        print(f"User said: {query}\n")
        return query.lower()
    except sr.UnknownValueError:
        print("Sorry, I did not get that. Please repeat.")
        speak("Sorry, I did not get that. Please repeat.")
        return "None"
    except sr.RequestError as e:
        print(f"Could not request results from Google Speech Recognition service; {e}")
        speak("Could not request results from Google Speech Recognition service. Please check your internet connection.")
        return "None"


def send_email(to, subject, body):
    # Sample email sending functionality using SMTP
    try:
        server = smtplib.SMTP('smtp.example.com', 587)
        server.starttls()
        server.login('your_email@example.com', 'your_password')
        message = f"Subject: {subject}\n\n{body}"
        server.sendmail('your_email@example.com', to, message)
        server.quit()
        print("Email has been sent!")
        speak("Email has been sent!")
    except Exception as e:
        print(f"Error sending email: {e}")
        speak("Sorry, I encountered an error while sending the email. Please try again later.")


if __name__ == "__main__":
    wish_me()
    speak("I am your assistant. Please tell me how may I help you")
    

    while True:
        query = take_command()

        if 'wikipedia' in query:
            speak('Searching Wikipedia...')
            query = query.replace("wikipedia", "")
            try:
                results = wikipedia.summary(query, sentences=2)
                speak("According to Wikipedia")
                print(results)
                speak(results)
            except wikipedia.exceptions.WikipediaException:
                print("Could not find information on Wikipedia.")
                speak("Could not find information on Wikipedia.")

        elif 'open youtube' in query:
            webbrowser.open("https://www.youtube.com")
            speak("Opening YouTube.")

        elif 'open google' in query:
            webbrowser.open("https://www.google.com")
            speak("Opening Google.")

        elif 'open gaana' in query:
            webbrowser.open("https://gaana.com")
            speak("Opening Gaana.")

        elif 'open my class' in query:
            webbrowser.open("https://myclass.lpu.in")
            speak("Opening My Class.")

        elif 'open ums' in query:
            webbrowser.open("https://ums.lpu.in")
            speak("Opening UMS.")

        elif 'what is the time' in query or 'tell me the time' in query:
            current_time = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"The time is {current_time}.")

        elif 'open code' in query:
            code_path = "C:\\Users\\PRINCE SINGH\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(code_path)
            speak("Opening Visual Studio Code.")
        elif 'fuck you' in query:
            speak("Diivakar You Fuck you Mother Fucker.")

        elif 'send email' in query:
            try:
                speak("To whom should I send the email?")
                to = take_command()
                speak("What is the subject of the email?")
                subject = take_command()
                speak("What should be the content of the email?")
                body = take_command()
                send_email(to, subject, body)
            except Exception as e:
                print(f"Error in email functionality: {e}")
                speak("Sorry, I encountered an error while processing your email request.")

        elif 'exit' in query or 'quit' in query:
            speak("Goodbye!")
            exit()

        else:
            speak("I'm sorry, I don't understand that command. Can you please repeat?")
