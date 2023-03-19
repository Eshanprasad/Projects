import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser
import os
import smtplib
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')       # this is the list of voices (returns the list of voices available)
engine.setProperty('voice', voices[1].id)
def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    hour = int(datetime.datetime.now().hour)       # 0 to 24
    if hour<12:
        speak("good morning")
    elif hour>=12 and hour<16:
        speak("good afternoon")
    else:
        speak("good evening")

def takeCommand():
    """
    It takes microphone input from the user
    :returns: string output
    """
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"User said: {query}\n")

    except Exception as e:
        # print(e)
        print("say that again please...")
        return "None"
    return query

def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('eshanprasad005@gmail.com', 'Esh@npr@s@d8885')
    server.sendmail('eshanprasad005@gmail.com', to, content)
    server.close()

if __name__ == '__main__':
    wishMe()
    speak("I am Jessy, Please tell me what I can do for you")

    # Logic for executing task based on query
    while True:
        query = takeCommand().lower()
        if 'wikipedia' in query:
            speak('Searching Wikipedia...')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences = 2)
            speak("According to wikipedia")
            print(results)
            speak(results)

        elif 'open youtube' in query:
            webbrowser.open("youtube.com")

        elif 'open google' in query:
            webbrowser.open("google.com")

        elif "play music" in query:
            music_dir = 'C:\\Users\\eshan\\Music'
            songs = os.listdir(music_dir)
            print(songs)
            os.startfile(os.path.join(music_dir, songs[0]))

        elif "the time" in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"the time is {strTime}")

        elif "open brave" in query:
            codepath = "C:\\ProgramData\\Microsoft\\Windows\\Start Menu\\Programs\\Brave.lnk"
            os.startfile(codepath)

        elif "email to khushi" in query:
            try:
                speak("what should I send?")
                content = takeCommand()
                to = "kushalprasad06@gmail.com"
                sendEmail(to, content)
                speak("Email has been sent!")
            except Exception as e:
                print(e)
                speak("sorry bhayya, I am not able to send this email")

        elif 'quit' in query:
            break
