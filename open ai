import openai
import streamlit as st

openai.api_key = "YOUR_API_KEY_HERE"

st.set_page_config(page_title="OpenAI Chat App", layout="centered")

st.title("OpenAI Chat App")

if "messages" not in st.session_state:
    st.session_state.messages = []

for msg in st.session_state.messages:
    with st.chat_message(msg["role"]):
        st.markdown(msg["content"])

user_input = st.chat_input("Type your message")

if user_input:
    st.session_state.messages.append({"role": "user", "content": user_input})
    with st.chat_message("user"):
        st.markdown(user_input)

    with st.chat_message("assistant"):
        message_placeholder = st.empty()
        message_placeholder.markdown("Thinking...")

    completion = openai.ChatCompletion.create(
        model="gpt-4o-mini",
        messages=st.session_state.messages,
        temperature=0.7,
    )

    reply = completion.choices[0].message["content"]
    st.session_state.messages.append({"role": "assistant", "content": reply})

    message_placeholder.markdown(reply)
