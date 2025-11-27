# Вгадай число 
Вгадай число. Програма генерує випадкове число від 1 до 100 (вам знадобиться import random).  Користувач намагається вгадати число. Програма підказує: "Більше" або "Менше". У користувача є лише 7 спроб. Якщо спроби закінчилися — гравець програв.

# Початок
    import random
    import tkinter as tk
    secret = random.randint(1, 100)  
    attempts = 7                     



# Перевірка вводу

    def check_guess():
        global attempts, secret

    guess_str = guess_entry.get()

   
    if not guess_str.isdigit():
        result_label.config(text="Введи число!")
        return

    guess = int(guess_str)

    
    if guess < secret:
        result_label.config(text="Більше!")
    elif guess > secret:
        result_label.config(text="Менше!")
    else:
        result_label.config(text="Молодець! Ти вгадав!")
        check_button.config(state="disabled")  
        return

    
    attempts -= 1
    attempts_label.config(text=f"Залишилось спроб: {attempts}")


    if attempts == 0:
        result_label.config(text=f"Не вийшло :( Число було: {secret}")
        check_button.config(state="disabled")



# Зіграти знову

    def restart_game():
        global secret, attempts

    secret = random.randint(1, 100)
    attempts = 7

    
    guess_entry.delete(0, tk.END)
    result_label.config(text="")
    attempts_label.config(text=f"Залишилось спроб: {attempts}")

    check_button.config(state="normal")  



# Валідація цифер

    def only_digits(char):
        return char.isdigit() or char == ""


# Вікно

    window = tk.Tk()
    window.title("Вгадай число")
    window.geometry("350x350")
    title_label = tk.Label(window, text="Вгадай число (1–100)", font=("Times New Roman", 14))
    title_label.pack(pady=10)


#Поле вводу

    validate_cmd = window.register(only_digits)

    guess_entry = tk.Entry(
        window,
        font=("Times New Roman", 12),
        validate="key",
        validatecommand=(validate_cmd, "%S")
    )
    guess_entry.pack(pady=5)

# Підтвердження через ENTER
    guess_entry.bind("<Return>", lambda event: check_guess())

    check_button = tk.Button(window, text="Перевірити", font=("Times New Roman", 12), command=check_guess)
    check_button.pack(pady=10)



# Зіграти знову
    restart_button = tk.Button(window, text="Зіграти знову", font=("Times New Roman", 12), command=restart_game)
    restart_button.pack(pady=5)


    result_label = tk.Label(window, text="", font=("Times New Roman", 12))
    result_label.pack(pady=5)

    attempts_label = tk.Label(window, text=f"Залишилось спроб: {attempts}", font=("Times New Roman", 12))
    attempts_label.pack(pady=5)

    window.mainloop()
