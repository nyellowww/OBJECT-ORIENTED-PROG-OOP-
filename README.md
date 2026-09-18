import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

       
        String[] items = {"Burger", "Fries", "Chicken with Rice", "Burger Steak", "Diet Pepsi"};
        double[] prices = {50.00, 35.00, 99.00, 85.00, 45.00};

        double totalAmount = 0;
        int totalQuantity = 0;

        char student = 'N';
        char again = 'Y';

        System.out.println("     CANTEEN ORDERING SYSTEM");
        System.out.println("MENU:");
        
        for (int i = 0; i < items.length; i++) {
            System.out.printf("%d. %s - ₱ %.2f%n",
                    i + 1, items[i], prices[i]);
        }
  
        while (again == 'Y' || again == 'y') {

            System.out.print("\nEnter item number (1-5): ");
            int item = input.nextInt();

            System.out.print("Enter quantity (1-10): ");
            int quantity = input.nextInt();

            System.out.print("Are you a student? (Y/N): ");
            student = input.next().charAt(0);
    
            if (item < 1 || item > 5 ||
                quantity < 1 || quantity > 10 ||
                (student != 'Y' && student != 'y' &&
                 student != 'N' && student != 'n')) {

                System.out.println("Invalid order! Please try again.");
                continue;
            }
        
            double amount = prices[item - 1] * quantity;

            totalAmount += amount;
            totalQuantity += quantity;

            System.out.printf("Added: %s x%d = ₱ %.2f%n",
                    items[item - 1], quantity, amount);

            System.out.print("Do you want to order again? (Y/N): ");
            again = input.next().charAt(0);

            while (again != 'Y' && again != 'y' &&
                   again != 'N' && again != 'n') {

                System.out.println("Invalid input!");
                System.out.print("Do you want to order again? (Y/N): ");
                again = input.next().charAt(0);
            }
        }

        double discountRate = 0;

        if ((student == 'Y' || student == 'y') && totalAmount >= 500) {
            discountRate = 0.15;
        } 
        else if (student == 'Y' || student == 'y') {
            discountRate = 0.10;
        } 
        else if (totalAmount >= 500) {
            discountRate = 0.05;
        }

        double deduction = totalAmount * discountRate;
        double finalAmount = totalAmount - deduction;

        System.out.println("\n     FINAL RECEIPT ");
        System.out.println("Total Quantity: " + totalQuantity);
        System.out.printf("Total Amount: ₱ %.2f%n", totalAmount);
        System.out.printf("Discount: %.0f%%%n", discountRate * 100);
        System.out.printf("Total Deduction: ₱ %.2f%n", deduction);
        System.out.printf("Final Amount to Pay: ₱ %.2f%n", finalAmount);
        System.out.println("=====================");

        input.close();
    }
}
