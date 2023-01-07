import openai
import pyperclip
import speech_recognition as sr
import winsound

# Replace YOUR_API_KEY with your actual API key
openai.api_key = "YOUR_API_KEY"

def get_speech_input():
    # Set up the speech recognizer
    recognizer = sr.Recognizer()

    # Capture the user's spoken question
    with sr.Microphone() as source:
        print("Say your question:")
        audio = recognizer.listen(source)

    # Convert the audio to text
    try:
        text = recognizer.recognize_google(audio)
        print(f"You said: {text}")
        return text
    except Exception as e:
        print("Sorry, I couldn't understand what you said.")
        return ""

def send_request(prompt):
    # Send a request to the ChatGPT API
    response = openai.Completion.create(
        engine="text-davinci-002",
        prompt=f"Proofread this text and fix punctuation and reword if needed: {prompt}",
        max_tokens=1024,
        n=1,
        temperature=0.5,
    )

    # Get the response text
    response_text = response["choices"][0]["text"]

    return response_text

def main():
    # Get the spoken input
    prompt = get_speech_input()

    # If no input was captured, exit the program
    if not prompt:
        return

    # Send a request to the ChatGPT API and get the response
    response_text = send_request(prompt)

    # Place the response in the clipboard
    pyperclip.copy(response_text)

    # Play a ding sound to indicate success
    winsound.PlaySound("SystemAsterisk", winsound.SND_ASYNC)

if __name__ == "__main__":
    main()
