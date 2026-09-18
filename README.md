import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        String[] items = {"Burger", "Fries", "Chicken", "Spaghetti", "Soft Drink"};
        double[] price = {50, 35, 75, 60, 25};

        double total = 0;
        int quantityTotal = 0;
        char student = 'N', again = 'Y';

        System.out.println("=== CANTEEN ORDERING SYSTEM ===");

        for (int i = 0; i < items.length; i++)
            System.out.printf("%d. %s - Php %.2f%n", i + 1, items[i], price[i]);

        while (again == 'Y' || again == 'y') {
            System.out.print("\nEnter item number (1-5): ");
            int item = input.nextInt();

            System.out.print("Enter quantity (1-10): ");
            int qty = input.nextInt();

            System.out.print("Are you a student? (Y/N): ");
            student = input.next().charAt(0);

            if (item < 1 || item > 5 || qty < 1 || qty > 10 ||
                (student != 'Y' && student != 'y' &&
                 student != 'N' && student != 'n')) {
                System.out.println("Invalid input!");
                continue;
            }

            double amount = price[item - 1] * qty;
            total += amount;
            quantityTotal += qty;

            System.out.printf("Added: %s x%d = Php %.2f%n",
                    items[item - 1], qty, amount);

            System.out.print("Order again? (Y/N): ");
            again = input.next().charAt(0);
        }

        double discount = 0;

        if ((student == 'Y' || student == 'y') && total >= 500)
            discount = .15;
        else if (student == 'Y' || student == 'y')
            discount = .10;
        else if (total >= 500)
            discount = .05;

        double deduction = total * discount;
        double finalAmount = total - deduction;

        System.out.println("\n=== FINAL RECEIPT ===");
        System.out.println("Total Quantity: " + quantityTotal);
        System.out.printf("Total: Php %.2f%n", total);
        System.out.printf("Discount: %.0f%%%n", discount * 100);
        System.out.printf("Deduction: Php %.2f%n", deduction);
        System.out.printf("Amount to Pay: Php %.2f%n", finalAmount);
        System.out.println("=====================");

        input.close();
    }
}
