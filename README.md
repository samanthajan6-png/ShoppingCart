# Super Shopping Quest

An interactive command-line shopping cart game written in Python. Add your
shopping loot, watch your cart total grow, and see if you unlock a checkout deal!

## Features

- Add items with their prices to a shopping cart.
- Playful shopping-quest prompts and checkout messages.
- Reject empty item names, non-numeric prices, and negative prices with friendly
  messages.
- Display the growing treasure list and running cart total after each item.
- Track progress toward the discount: spend over $50 to unlock 10% off.
- Print a grand checkout receipt, or a friendly message if the cart is empty.

## Requirements

- Python 3
- No third-party packages required

## Run the Program

Save the source code below as `main.py`, then run it from a terminal:

```bash
python3 main.py
```

Enter an item and its price when prompted. Type `done` when you are ready to
check out. The 10% discount applies only when your subtotal is over $50.

## Source Code

```python
# Main py
# Shopping Cart tracker

# Samantha Kaiser


def calculate_total(cart):
    """Function to calculate total cost and apply a 10% discount if total is over $50."""
    subtotal = sum(cart.values())
    if subtotal > 50:
        discount = subtotal * 0.10
        final_total = subtotal - discount
        discount_applied = True
    else:
        discount = 0
        final_total = subtotal
        discount_applied = False

    return subtotal, discount, final_total, discount_applied


# dictionary: to store items and their prices
shopping_cart = {}

print("=" * 42)
print("       WELCOME TO THE SUPER SHOPPING QUEST!")
print("  Add your loot, then see if you unlock a deal!")
print("=" * 42)

# loop: a while loop to continuously collect user input
while True:
    item = input("\nWhat treasure are we adding? (type 'done' to check out): ")
    if item.lower() == 'done':
        break

    if not item:
        print("Your cart quest needs an item name. Give it another try!")
        continue

    try:
        price = float(input(f"Enter the price for {item}: $"))
    except ValueError:
        print("That price is a mystery! Please enter a number.")
        continue

    if price < 0:
        print("Negative prices? Nice try! Please enter zero or more.")
        continue

    # updating dictionary with the user's input
    shopping_cart[item] = price

    # loop and meaningful output: to display the items in the cart and their prices
    if shopping_cart:
        cart_total = sum(shopping_cart.values())
        print("\n" + "-" * 42)
        print("YOUR TREASURE SO FAR")
        print("-" * 42)

        for item_name, item_price in shopping_cart.items():
            print(f"  * {item_name}: ${item_price:.2f}")

        print("-" * 42)
        print(f"Cart total: ${cart_total:.2f}")
        if cart_total <= 50:
            print(f"Only ${50.01 - cart_total:.2f} more to unlock 10% off!")
        else:
            print("Deal unlocked! Your 10% discount is ready for checkout!")

if not shopping_cart:
    print("\nNo loot collected this time. Your wallet can relax!")
else:
    subtotal, discount, final_total, discount_applied = calculate_total(shopping_cart)
    print("\n" + "=" * 42)
    print("          THE GRAND CHECKOUT")
    print("=" * 42)
    for item_name, item_price in shopping_cart.items():
        print(f"  * {item_name}: ${item_price:.2f}")
    print("-" * 42)
    print(f"Subtotal:             ${subtotal:.2f}")
    print(f"Super-saver discount: -${discount:.2f}")
    print(f"Your grand total:      ${final_total:.2f}")
    if discount_applied:
        print("Jackpot! You unlocked the 10% discount!")
    else:
        print("So close! Spend over $50 next time for 10% off.")
    print("Thanks for shopping. Have a cart-tastic day!")
    print("=" * 42)
```
