mport telebot
import random

bot = telebot.TeleBot('7750207742:AAEv4HZnMEyAjEoC1vOd7tpgVxYucqzvbcc')

@bot.message_handler(commands=['start'])
def handle_start(message):
    bot.reply_to(message, "Привет!😊 Я самый простой бот, которого можно добавить в любой чат. Используйте команду /help для получения списка команд.")
# хелп
@bot.message_handler(commands=['help'])
def handle_help(message):
    bot.reply_to(message,
                 "Доступные команды:\n"
                 "/start - Начать\n"
                 "/help - Список команд\n"
                 "/roll - Рандом число (0-100)\n"
                 "/flip - Подбросить монетку (орёл/решка)\n"
                 "/quote - Вывести случайную цитату\n"
                 "/fact - Интересный факт о человеке\n"
                 "/repeat [текст] - Повторить ваш текст"
                 )
# рандом число
@bot.message_handler(commands=['roll'])
def handle_roll(message):
    bot.reply_to(message, f"Результат рандомного числа: {random.randint(0,100)}")
      
# монетка
@bot.message_handler(commands=['flip'])
def handle_flip(message):
    result = random.choice(["Орёл", "Решка"])
    bot.reply_to(message, f"Результат подбрасывания монетки: {result}")
# топ цитаты
@bot.message_handler(commands=['quote'])
def handle_quote(message):
    quotes = [
        "Кто рано встает — тому весь день спать хочется.",
        "Если закрыть глаза, становится темно.",
        "Тут — это вам не там."
        "Если заблудился в лесу, иди домой."
        "Делай, как надо. Как не надо, не делай."
    ]
    bot.reply_to(message, random.choice(quotes))
# топ факты
@bot.message_handler(commands=['fact'])
def handle_fact(message):
    facts = [
        "Емкость мозга человека превышает 4 терабайта.",
        "Ваш череп состоит из 29 различных костей.",
        "При чихании все функции организма останавливаются, даже сердце."
        "Человек забывает 90% своих снов."
        "Ногти на пальцах рук растут примерно в 4 раза быстрее, чем на пальцах ног."
        "У блондинов борода растет быстрее, чем у брюнетов."
    ]
    bot.reply_to(message, random.choice(facts))
# повторялка
@bot.message_handler(commands=['repeat'])
def handle_repeat(message):
    try:
        text = message.text.split()[1:] # извлекаем текст после команды /repeat
        repeated_text = " ".join(text)
        bot.reply_to(message, repeated_text)
    except IndexError:
        bot.reply_to(message, "Пж, укажите текст для повторения после /repeat")


@bot.message_handler(func=lambda message: True)
def handle_unknown(message):
    bot.reply_to(message, "Сори, неверная команда. Список команд /help.")


bot.infinity_polling()
