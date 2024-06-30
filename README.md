import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class InvoiceGenerator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Invoice invoice = new Invoice();

        System.out.println("Welcome to Invoice Generator");

        while (true) {
            System.out.println("\nMENU:");
            System.out.println("1. Add Item to Invoice");
            System.out.println("2. Generate Invoice");
            System.out.println("3. Exit");

            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter item description: ");
                    String description = scanner.nextLine();

                    System.out.print("Enter unit price: ");
                    double price = scanner.nextDouble();

                    System.out.print("Enter quantity: ");
                    int quantity = scanner.nextInt();

                    InvoiceItem item = new InvoiceItem(description, price, quantity);
                    invoice.addItem(item);
                    System.out.println("Item added to invoice.");
                    break;
                case 2:
                    // Generate and display invoice
                    System.out.println("\nINVOICE:");
                    for (InvoiceItem invoiceItem : invoice.getItems()) {
                        System.out.println(invoiceItem);
                    }
                    System.out.printf("\nTOTAL: $%.2f\n", invoice.getTotal());
                    break;
                case 3:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please enter again.");
            }
        }
    }
}

class InvoiceItem {
    private String description;
    private double price;
    private int quantity;

    public InvoiceItem(String description, double price, int quantity) {
        this.description = description;
        this.price = price;
        this.quantity = quantity;
    }

    public double getTotal() {
        return price * quantity;
    }

    @Override
    public String toString() {
        return String.format("%s - $%.2f x %d = $%.2f", description, price, quantity, getTotal());
    }
}

class Invoice {
    private List<InvoiceItem> items;

    public Invoice() {
        this.items = new ArrayList<>();
    }

    public void addItem(InvoiceItem item) {
        items.add(item);
    }

    public List<InvoiceItem> getItems() {
        return items;
    }

    public double getTotal() {
        double total = 0;
        for (InvoiceItem item : items) {
            total += item.getTotal();
        }
        return total;
    }
}

