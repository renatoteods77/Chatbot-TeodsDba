# Chatbot-TeodsDba
Chatbot para DBA Oracle: Ganhe Tempo e Eficiência



Instalando SDK do Google

#Instalando o SDK do Google
!pip install -q -U google-generativeai

API KEY do google IA STUDIO

#Configurações iniciais
import google.generativeai as genai

GOOGLE_API_KEY="API KEY"
genai.configure(api_key=GOOGLE_API_KEY)

LISTAGEM DOS MODELOS DISPONIVEIS

#Listando os modelos disponíveis
for m in genai.list_models():
  if 'generateContent' in m.supported_generation_methods:
    print(m.name)

generation_config = {
  "candidate_count": 1,
  "temperature": 0.5,
}

safety_settings={
    'HATE': 'BLOCK_NONE',
    'HARASSMENT': 'BLOCK_NONE',
    'SEXUAL' : 'BLOCK_NONE',
    'DANGEROUS' : 'BLOCK_NONE'
    }

model = genai.GenerativeModel(model_name='gemini-1.0-pro',
                                  generation_config=generation_config,
                                  safety_settings=safety_settings,)

response = model.generate_content("crie todo o codigo do meu proprio chtabot juntando com todas inteligências artificiais exitente")
print(response.text)

Comando while aguardando parada do chat

chat = model.start_chat(history=[])

prompt = input('Esperando prompt: ')

while prompt != "fim":
  response = chat.send_message(prompt)
  print("Resposta:", response.text, '\n\n')
  prompt = input('Esperando prompt: ')

chat

chat.history

#Melhorando a visualização
#Código disponível em https://ai.google.dev/tutorials/python_quickstart#import_packages
import textwrap
from IPython.display import display
from IPython.display import Markdown

def to_markdown(text):
  text = text.replace('•', '  *')
  return Markdown(textwrap.indent(text, '> ', predicate=lambda _: True))

#Imprimindo o histórico
for message in chat.history:
  display(to_markdown(f'**{message.role}**: {message.parts[0].text}'))
  print('-------------------------------------------')
