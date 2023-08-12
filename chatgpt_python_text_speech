import openai
import speech_recognition as sr

# Set up your OpenAI API key
openai.api_key = 'YOUR_OPENAI_API_KEY' //Write yours e.g:- gfdshFSRgfdhWSHFNDCfzytQWSDRFGVZbnx

# Set up the Speech Recognition recognizer
recognizer = sr.Recognizer()

# Define the OpenAI model
MODEL = "gpt-3.5-turbo"

def get_user_input_from_speech():
    with sr.Microphone() as source:
        print("Speak something...")
        audio = recognizer.listen(source)

    try:
        user_input = recognizer.recognize_google(audio)
        return user_input
    except sr.UnknownValueError:
        print("Sorry, I could not understand your speech.")
        return None
    except sr.RequestError:
        print("Sorry, there was an error connecting to the Google API.")
        return None

def generate_openai_response(messages):
    response = openai.ChatCompletion.create(
        model=MODEL,
        messages=messages,
        temperature=0,
    )
    return response.choices[0].message.content

def main():
    print("Welcome to the AI-Enhanced Console!\n")
    
    while True:
        print("Please select an option:")
        print("1. Text input")
        print("2. Speech input")
        print("3. Exit")
        
        choice = input("Enter the number of your choice: ")
        
        if choice == "1":
            user_input = input("Enter your prompt: ")
        elif choice == "2":
            user_input = get_user_input_from_speech()
            if not user_input:
                continue
        elif choice == "3":
            print("Exiting...")
            break
        else:
            print("Invalid choice. Please select a valid option.")
            continue

        messages = [
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": user_input},
        ]
        response = generate_openai_response(messages)
        print("AI:", response)

if __name__ == "__main__":
    main()
