# ImageModeratorBot
____

```python
import logging
from aiogram import Bot, Dispatcher, executor,types
import requests
import json


API_TOKEN = ''

logging.basicConfig(level=logging.INFO)

# Initialize bot and dispatcher
bot = Bot(token=API_TOKEN)
dp = Dispatcher(bot)



@dp.message_handler(commands=['start', 'help'])
async def send_welcome(message: types.Message):
    await message.reply("Привет!\nЯ бот-модератор изображений !\nДля использования отправте фотографию для проверки в чат")

#nudity-2.0,offensive,gore





@dp.message_handler(content_types=['photo'])
async def handle_docs_photo(message):
    await message.photo[-1].download('test.jpg')
    params = {
  'models': 'nudity-2.0,offensive,gore',
  'api_user': '1522578665',
  'api_secret': 'vpUAgfzgk5uVZCUZzKUo'}
    files = {'media': open('test.jpg', 'rb')}
    r = requests.post('https://api.sightengine.com/1.0/check.json', files=files, data=params)
    output = json.loads(r.text)
    n1 = output['nudity']['sexual_activity']
    n2 = output['nudity']['suggestive']
    n3 = output['nudity']['sexual_display']
    n4 = output['nudity']['erotica']
    n5 = output['offensive']['nazi']
    n6 = output['offensive']['supremacist']
    n7 = output['offensive']['confederate']
    n8 = output['offensive']['middle_finger']
    n9 = output['offensive']['terrorist']
    n10 = output['gore']['prob']
    await message.reply(f"Сексуальная активность: {int(n1*100)}%\nЭротика: {int(n2*100)}%\nСексуальная демонстрация: {int(n3*100)}%\nСимволы нацистской эпохи: {int(n5*100)}%\nСимволы превосходства: {int(n6*100)}%\nКонфедеративные символы: {int(n7*100)}%\nСредний палец: {int(n8*100)}%\nСимволы террормзма: {int(n9*100)}%\nКровь и насилие: {int(n10*100)}%")
    
    
    
    
    
    
    
       
if __name__ == '__main__':
    executor.start_polling(dp, skip_updates=True)
    
```
