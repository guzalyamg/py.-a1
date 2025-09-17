# py.-a1
assignmetn 1 from computer languages 
# Checkout Program

assignemt was about writing a code to cashier.  
What it does?, it asks user to enter the item name, its price, quantity. And when you leave the item name like blank, then it stops asking and shows you receipt.  

---

## Now how it works?
The program adds up all the items to get a subtotal, and if the subtotal is 100 or more, it gives a 10% discount,  then adds 6% sales tax on the amount after discount. and at the end, it prints a receipt with the:
   - Number of items
   - Subtotal
   - Discount
   - Tax
   - Total
---

 - subtotal = add_line(subtotal, price, qty) -- This line updates the subtotal by adding the price × quantity of the item you just entered. It calls the function add_line from core.py to keep the math separate from the input/output.
 - if name == "": break --  checks if the user pressed Enter without typing an item name, and If yes, the loop stops and the program goes to print the receipt.
 - discount = compute_discount(subtotal) -- it calls a function that decides if a 10% discount should be appl
 - taxable = subtotal - discount --  means that the tax is calculated after subtracting the discount, but not on the full subtotal.
 - print(f"Subtotal: ${format_money(subtotal)}")  -- the f"" part is called an f-string, it makes it easy to put numbers inside text, and the function format_money makes sure that the number always has 2 decimals, like 7.40.


---
EXAMPLE the result I got from the code

Item name (blank for finish): water
Unit price: 50
Quantity: 3
Item name (blank for finish): 
------- RECEIPT -------
items: 1
subtotal: $150.00
discount: $15.00
tax: $8.10
TOTAL: $143.10

--- 
HERE IS THE CODE
# for the  main.py



from core import add_line, compute_discount, compute_tax, format_money


def run_checkout():
    subtotal = 0.0
    item_count = 0



    while True:
        name = input("Item name (blank for finish): ").strip()
        if name == "":
            break
        price = float(input("Unit price: ").strip())
        qty = int(input("Quantity: ").strip())

        subtotal = add_line(subtotal, price, qty)
        item_count += 1


    discount = compute_discount(subtotal)
    taxable = subtotal - discount
    tax = compute_tax(taxable)
    total = taxable + tax



    print("------- RECEIPT -------")
    print(f"items: {item_count}")
    print(f"subtotal: ${format_money(subtotal)}")
    print(f"discount: ${format_money(discount)}")
    print(f"tax: ${format_money(tax)}")
    print(f"TOTAL: ${format_money(total)}")



if __name__ == "__main__":
    run_checkout()
---
# core.py



def add_line(subtotal: float, price: float, qty: int) -> float:
    """returns new subtotal after add price*qty."""
    return subtotal + (price * qty)



def compute_discount(subtotal: float) -> float:
    """returns 10% of subtotal if subtotal >= 100 else is 0."""
    if subtotal >= 100:
        return subtotal * 0.10
    return 0.0



def compute_tax(amount: float) -> float:
    """returns 6% of given amount subtotal - discount"""
    return amount * 0.06



def format_money(x: float) -> str:
    """returns string with exactly 2 decimals  """
    return f"{x:.2f}"






