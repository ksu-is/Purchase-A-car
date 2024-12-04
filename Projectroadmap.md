def calculate_savings_for_car():
    # Ask the user for the car's price and their savings details
    car_price = float(input("Enter the total price of the car: $"))
    savings = float(input("Enter the amount you already have saved: $"))
     # Ask if they want to pay in full or finance the car
    choice = input("Do you want to pay in full or finance the car? (full/finance): ").lower()

    if choice == 'full':
        # Calculate how much more they need to save
        remaining_amount = car_price - savings
        if remaining_amount <= 0:
            print("You have enough savings to buy the car in full!")
        else:
            print(f"You need to save an additional ${remaining_amount:.2f} to buy the car in full.")
            
            # Ask how much the user can save per month
            monthly_savings = float(input("How much can you save per month? $"))
            if monthly_savings <= 0:
                print("You need to save more each month to make progress toward your goal.")
            else:
                # Calculate how many months it will take to save the remaining amount
                months_needed = remaining_amount / monthly_savings
                print(f"To save ${remaining_amount:.2f}, it will take you {months_needed:.0f} months.")

    elif choice == 'finance':
        # Ask for financing details
        down_payment = float(input("Enter the down payment amount: $"))
        loan_term_years = int(input("Enter the loan term in years: "))
        
        # Ask for credit score and adjust interest rate
        credit_score = int(input("Enter your credit score: "))
        if credit_score >= 750:
            interest_rate = 3  # Excellent credit score
        elif credit_score >= 700:
            interest_rate = 5  # Good credit score
        elif credit_score >= 650:
            interest_rate = 7  # Fair credit score
        else:
            interest_rate = 10  # Poor credit score
        
        print(f"Based on your credit score of {credit_score}, your interest rate is {interest_rate}%.")

        # Calculate the financed amount (car price minus down payment)
        financed_amount = car_price - down_payment
        
        # Monthly interest rate and total number of payments
        monthly_interest_rate = (interest_rate / 100) / 12
        total_payments = loan_term_years * 12
        
        # Calculate the monthly payment using the formula for an amortized loan
        if monthly_interest_rate != 0:
            monthly_payment = (financed_amount * monthly_interest_rate) / (1 - (1 + monthly_interest_rate) ** -total_payments)
        else:
            # If interest rate is 0%, just divide the amount by months
            monthly_payment = financed_amount / total_payments
        
        print(f"Your monthly payment will be: ${monthly_payment:.2f}")
        total_cost = down_payment + (monthly_payment * total_payments)
        print(f"Over the course of {loan_term_years} years, the total cost of the car will be: ${total_cost:.2f}")
        
    else:
        print("Invalid choice. Please enter 'full' or 'finance'.")

# Call the function
calculate_savings_for_car()

