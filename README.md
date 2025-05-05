import random

def spin_slots():
    symbols = ['🍒', '🍋', '😈', '🍉', '⭐', '💎']
    return [random.choice(symbols) for _ in range(3)]

def check_win(spin_result):
    if spin_result[0] == spin_result[1] == spin_result[2]:
        return True
    return False

def casino_slots():
    print("Добро пожаловать в Казино Слоты!")
    balance = 1000000  # Начальный баланс игрока
    min_bet = 5000   # Минимальная ставка

    while True:
        print(f"\nВаш текущий баланс: ${balance}")
        print(f"Минимальная ставка: ${min_bet}")
        bet = input("Введите сумму для ставки (или 'выход' для выхода): ")

        if bet.lower() == 'выход':
            print("Спасибо за игру! Ваш баланс: $", balance)
            break

        try:
            bet = int(bet)
            if bet < min_bet:
                print(f"Ставка должна быть не менее ${min_bet}.")
                continue
            if bet <= 0:
                print("Ставка должна быть положительным числом.")
                continue
            if bet > balance:
                print("У вас недостаточно средств для этой ставки.")
                continue
        except ValueError:
            print("Пожалуйста, введите корректную сумму.")
            continue

        # Вращение слотов
        spin_result = spin_slots()
        print("Результат вращения:", ' '.join(spin_result))

        # Проверка результата
        if check_win(spin_result):
            print(f"Поздравляем! Вы выиграли ${bet * 20}!")
            balance += bet * 5  # Увеличиваем баланс на сумму выигрыша
        else:
            print(f"К сожалению, вы не выиграли. Вы потеряли ${bet}.")
            balance -= bet  # Уменьшаем баланс на сумму ставки

        # Проверка, остались ли средства
        if balance <= 0:
            print("Вы проиграли все свои деньги! Игра окончена.")
            break

if __name__ == "__main__":
    casino_slots()
