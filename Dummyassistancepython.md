# dummyassistance
import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import smtplib



engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
#print(voices[1].id)
engine.setProperty('voice', voices[0].id)
def speak(audio):
    engine.say(audio)
    engine.runAndWait()
def wishMe():
    hour = int(datetime.datetime.now().hour)

    if hour>=0 and hour<12:
        speak("Good morning!")
    elif hour>=12 and hour<18:
        speak("Good afternoon!")

    else:
        speak("Good evening !")


    speak("I am your assistance. Please tell how may I help you")
def takecommand():
    # takes microphone input

    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening....")
        r.pause_threshold = 1

        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"User said: , {query}\n")

    except Exception as e:
        #print(e)
        print("say that again please...")
        return "None"
    return query


def sendEmail(to, content):
    server = smtplib.SMTP('SMTP.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('snghprince2000@gmail.com', 'your-password-here')
    server.sendmail(snghprince2000@gmail.com, to, content)
    server.close()

if __name__ == '__main__':
    wishMe()
    #while True:
    if 1:
        query = takecommand().lower()
    #excuting task
        if 'wikipedia' in query:
            speak('searching wikipedia...')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=2)
            speak("According to wikipedia")
            print(results)
            speak(results)

        elif 'open youtube' in query:
            webbrowser.open("youtube.com")
        elif 'open google' in query:
            webbrowser.open("google.com")
        elif 'open ganna' in query:
            webbrowser.open("ganna.com")
        elif 'open my class' in query:
            webbrowser.open("myclass.lpu.in")
        elif 'open u m s' in query:
            webbrowser.open("ums.lpu.in")



        # elif 'play music' in query:
        #     music_dir =




        elif 'what the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"The time is {strTime}")


        elif 'open code' in query:
            codePath = "C:\\Users\\PRINCE SINGH\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codePath)
