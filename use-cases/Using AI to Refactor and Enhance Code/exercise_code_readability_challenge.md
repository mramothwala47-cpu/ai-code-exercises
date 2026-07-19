# Exercise: Code Readability Challenge (Python)

## Selected Exercise
**Example 4: Poor Formatting and Structure (Python)**



# Step 1: Understanding the Original Code
The original `discount()` function calculates the final purchase amount for an e-commerce shopping cart. It:

- Calculates the cart total.
- Applies promotional discounts.
- Applies customer loyalty discounts.
- Enables free shipping when applicable.
- Returns the original amount, discount amount, final amount, and shipping status.

The provided unit tests were executed before refactoring to understand the expected behavior.

**Result:**  All tests passed.



# Step 2: AI Prompt Used
> Review the following Python function and improve its readability without changing its functionality. Focus on formatting, indentation, spacing, meaningful variable names, and logical organization. Keep the behavior exactly the same so that all existing unit tests continue to pass.



# Step 3: Refactored Code

```python
def discount(cart, promos, user):
    discount_amount = 0
    cart_total = 0

    # Calculate total cart value
    for item in cart:
        cart_total += item["price"] * item["quantity"]

    # Process promotional discounts
    for promo in promos:

        if (
            promo["type"] == "percent"
            and (
                promo["min_purchase"] is None
                or cart_total >= promo["min_purchase"]
            )
        ):
            value = cart_total * promo["value"] / 100
            discount_amount = max(discount_amount, value)

        elif (
            promo["type"] == "fixed"
            and (
                promo["min_purchase"] is None
                or cart_total >= promo["min_purchase"]
            )
        ):
            value = min(promo["value"], cart_total)
            discount_amount = max(discount_amount, value)

        elif (
            promo["type"] == "shipping"
            and cart_total >= promo["min_purchase"]
        ):
            user["free_shipping"] = True

    # Apply loyalty discounts
    if user["status"] == "vip":
        loyalty_discount = cart_total * 0.05
        discount_amount = max(discount_amount, loyalty_discount)

    elif (
        user["status"] == "member"
        and user["months"] > 6
    ):
        loyalty_discount = cart_total * 0.02
        discount_amount = max(discount_amount, loyalty_discount)

    return {
        "original": cart_total,
        "discount": discount_amount,
        "final": cart_total - discount_amount,
        "free_shipping": user.get("free_shipping", False),
    }
```


# Step 4: Verify Functionality

The unit tests were run again after refactoring.

## Test Results

| Test | Result |
|------|--------|
| Percentage Discount | Passed |
| Fixed Discount | Passed |
| Free Shipping | Passed |
| VIP Discount | Passed |
| Member Discount | Passed |
| Best Discount Selection | Passed |

**Overall Result:** All tests passed successfully.



# Readability Improvements
The following improvements were made:

- Added proper indentation.
- Added whitespace between logical sections.
- Renamed cryptic variables.
- Added comments explaining each section.
- Split long conditional statements across multiple lines.
- Improved return statement formatting.
- Used descriptive variable names.



# Variable Name Improvements

| Original | Improved |
|-----------|-----------|
| d | discount_amount |
| tot | cart_total |
| i | item |
| p | promo |
| val | value |
| vd | loyalty_discount |

These names immediately communicate the purpose of each variable.

---

# Would Breaking the Function into Smaller Functions Help?
Yes.

The function could be divided into helper functions such as:

- `calculate_cart_total()`
- `apply_promotional_discounts()`
- `apply_loyalty_discount()`
- `apply_shipping_discount()`

This would improve readability, maintainability, and make each part easier to test independently.



# Reflection Questions

## 1. How much easier is the code to understand now?
The refactored version is much easier to read because each section performs one logical task. The improved spacing, comments, and descriptive variable names make the code easier to follow.



## 2. What readability issues did the AI catch?
The AI identified several readability issues:

- Poor variable names.
- Multiple statements on one line.
- Inconsistent spacing.
- Long conditional statements.
- Lack of comments.
- Poor overall formatting.



## 3. What readability issues did the AI miss?

The AI did not fully recommend separating the logic into smaller helper functions. While the formatting improved significantly, the function could still be decomposed into smaller reusable components.



## 4. Which readability improvements had the biggest impact?
The biggest improvements were:

- Renaming variables.
- Proper indentation.
- Adding comments.
- Organizing the code into logical sections.

These changes made the function's purpose much clearer.



## 5. How did the improved names change your understanding?

Descriptive names such as `cart_total`, `discount_amount`, and `loyalty_discount` immediately explain what each value represents, reducing the need to inspect every line of code.



## 6. What readability patterns can you apply in future code?
Future code should follow these practices:

- Use meaningful variable names.
- Keep one statement per line.
- Group related logic together.
- Add comments where helpful.
- Use consistent indentation and spacing.
- Break large functions into smaller reusable functions.
- Keep conditional statements readable.



# Conclusion
This demonstrated that improving readability does not require changing functionality. By applying better formatting, meaningful naming, and clearer organization, the code became significantly easier to understand while preserving its original behavior.

**Final Status:** Refactoring completed successfully and all unit tests continue to pass.
