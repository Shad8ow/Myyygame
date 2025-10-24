import random

# Початкові параметри
city = {
    "residents": 5,
    "happiness": 5,  # від 0 до 10
    "gold": 10,
    "spells": ["Світло ночі"],
}

day = 1

def show_status():
    print(f"\n=== День {day} ===")
    print(f"Мешканці: {city['residents']} (Щастя: {city['happiness']}/10)")
    print(f"Золото: {city['gold']}")
    print(f"Закляття: {', '.join(city['spells'])}")

def random_event():
    event = random.choice([
        "напад лісових монстрів",
        "прибуток від торгівлі",
        "невдалий експеримент",
        "знахідка артефакту",
        "спокійний день"
    ])
    return event

def process_event(event):
    if event == "напад лісових монстрів":
        loss = random.randint(1, 3)
        city["residents"] = max(0, city["residents"] - loss)
        city["happiness"] = max(0, city["happiness"] - 2)
        print(f"Увага! Був {event}. Ви втратили {loss} мешканців і щастя знизилось.")
    elif event == "прибуток від торгівлі":
        gain = random.randint(5, 15)
        city["gold"] += gain
        city["happiness"] += 1
        print(f"Вдалий день! {event}. Ви отримали {gain} золота і мешканці стали щасливішими.")
    elif event == "невдалий експеримент":
        city["happiness"] = max(0, city["happiness"] - 1)
        print(f"{event}. Ніхто не постраждав, але щастя мешканців трохи впало.")
    elif event == "знахідка артефакту":
        new_spell = f"Закляття {random.randint(1,100)}"
        city["spells"].append(new_spell)
        city["happiness"] += 1
        print(f"Ура! {event}. Ви отримали нове закляття: {new_spell}")
    else:
        print("Спокійний день. Мешканці раді і відпочивають.")

def play_day():
    global day
    show_status()
    print("\nВаріанти дій:")
    print("1. Дослідити ліс")
    print("2. Покращити будівлі")
    print("3. Експериментувати в лабораторії")
    print("4. Торгувати на ринку")
    
    # Автовибір дії
    action = random.choice([1,2,3,4])
    print(f"\nВи обрали дію: {action}")
    
    event = random_event()
    process_event(event)
    
    # Підтримка ліміту щастя
    city["happiness"] = min(10, city["happiness"])
    
    day += 1

# Основний цикл гри
while city["residents"] > 0 and city["happiness"] > 0 and day <= 10:
    play_day()

# Підсумок гри
print("\n=== Кінець гри ===")
if city["residents"] <= 0:
    print("Всі мешканці покинули місто. Гру завершено.")
elif city["happiness"] <= 0:
    print("Мешканці занадто нещасні. Місто занепало.")
else:
    print("10 днів минуло! Місто процвітало, мешканці щасливі!")
print(f"Мешканці: {city['residents']}, Щастя: {city['happiness']}, Золото: {city['gold']}, Закляття: {', '.join(city['spells'])}")

