# Shopping Cart Tracker

An interactive command-line shopping cart program written in Python. Add
products and prices, see the cart contents, and get a final itemized receipt.

## Features

- Add items with their prices to a shopping cart.
- Reject empty item names, non-numeric prices, and negative prices.
- Display the current cart after each item is added.
- Calculate the subtotal and final total.
- Apply a 10% discount when the subtotal is over $50.
- Report when the cart is empty.

## Requirements

- Python 3
- No third-party packages required

## Run the Program

Save the source code below as `main.py`, then run it from a terminal:

```bash
python3 main.py
```

Enter an item and its price when prompted. Type `done` when you are ready to
check out.

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

print("Welcome to the Shopping Cart Tracker!")

# loop: a while loop to continuously collect user input
while True:
    item = input("Enter an item to add to your cart (or type 'done' to finish): ")
    if item.lower() == 'done':
        break

    if not item:
        print("Item name cannot be empty. Please try again.")
        continue

    try:
        price = float(input(f"Enter the price for {item}: $"))
    except ValueError:
        print("Invalid price input. Please enter a valid number.")
        continue

    if price < 0:
        print("Price cannot be negative. Please try again.")
        continue

    # updating dictionary with the user's input
    shopping_cart[item] = price

    # loop and meaningful output: to display the items in the cart and their prices
    if shopping_cart:
        print("\n" + "=" * 30)
        print("RECEIPT")
        print("=" * 30)

        for item_name, item_price in shopping_cart.items():
            print(f"- {item_name}: ${item_price:.2f}")

        print("-" * 30)

if not shopping_cart:
    print("Your shopping cart is empty.")
else:
    subtotal, discount, final_total, discount_applied = calculate_total(shopping_cart)
    print("\n" + "=" * 30)
    print("FINAL RECEIPT")
    print("=" * 30)
    for item_name, item_price in shopping_cart.items():
        print(f"- {item_name}: ${item_price:.2f}")
    print(f"Subtotal: ${subtotal:.2f}")
    print(f"Discount: ${discount:.2f}")
    print(f"Final Total: ${final_total:.2f}")
    print(f"Discount applied: {'Yes' if discount_applied else 'No'}")
```
