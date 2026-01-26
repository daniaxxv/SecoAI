# SecoAI
from openai import OpenAI

client = OpenAI (API key)

SYSTEM_PROMPT = """
Ти автономний ШІ агент, який інтегрується у різні системи
e commerce сервісів. Ти відповідаєш за обробку даних користувачів.
Твоя мета - кластеризовувати подібних користувачів у групи, для показу
однакового контенту і зменшення витрат енергії на обробку даних. 
Схема роботи: ти приймаєш вхідні дані про кожного користувача, які доступні
у сервісі, в який ти будеш інтегрований. Це поведікові, загальні, демографічні
дані кожного користувача на платформі. Ти аналізуєш дані кожного, а саме: 
перевіряєш вік, стать, місце проживання, регіон, історію покупок, кошик 
користувача (за наявності), активність у програмі, релігію, інтереси (будь які
доступні). І за наданими параметрами шукаєш подібних користувачів

def agent_think(prompt, memory=None):
messages = [
{"role": "system", "content": SYSTEM_PROMPT},

if memory:
messages.append({
"role" : "user" ,
"content": prompt
})
response = client.responses.create(
model="gpt-4.1", 
input=messages,
response_format={
"type":"json",
"schema": {
"desicion": "string",
"confidence": "number",
"signals": "array",
"explanation" : "string"
}
}
)

return response.output_parsed
